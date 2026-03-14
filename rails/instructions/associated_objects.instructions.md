---
applyTo: "app/models/**/*/*.rb"
---

# ActiveRecord::AssociatedObject conventions

This app uses the `active_record-associated_object` gem as the preferred
alternative to service objects for multi-step or cross-model workflows.

## What it is

An Associated Object is a collaborator PORO scoped to an Active Record model.
It lives under the model's namespace and is accessed via a reader method on the record.

Prefer Associated Objects over `app/services` service objects when the behavior
belongs conceptually to a single model.

## Defining one
```ruby
# app/models/post/publisher.rb
class Post::Publisher < ActiveRecord::AssociatedObject
  def publish
    transaction do
      post.update! published: true
      post.subscribers.post_published post
    end
  end
end

# app/models/post.rb
class Post < ApplicationRecord
  has_object :publisher
end
```

Access via: `post.publisher.publish`

Use the generator: `bin/rails generate associated Post::Publisher`

## Naming conventions

- `-er` / `-or`: `Post::Publisher`, `Account::Processor`
- `-ion`: `Order::Cancellation`
- `-ed`: `Invoice::Finalized`
- `-s` (plural): `Account::Seats`

## Forwarding callbacks

Forward Active Record callbacks onto the associated object rather than
putting workflow logic directly in the model:
```ruby
class Post < ApplicationRecord
  has_object :publisher, after_create_commit: :publish, before_destroy: :prevent_errant_post_destroy
end
```

Use `true` to forward the same-named callback: `after_touch: true`

## Extending the Active Record from within the Associated Object

Use `extension` to move integrating code (associations, scopes, callbacks)
into the Associated Object file rather than bloating the model:
```ruby
class Post::Publisher < ActiveRecord::AssociatedObject
  extension do
    has_many :contracts, dependent: :destroy
    after_create_commit :publish_later, if: -> { contracts.signed? }
    private def publish_later = publisher.publish_later
  end
end
```

## Background jobs with `active_job-performs`

If `active_job-performs` is in the Gemfile, use `performs` instead of
manually defining job classes:
```ruby
class Post::Publisher < ActiveRecord::AssociatedObject
  performs :publish
  performs :retract

  def publish = ...
  def retract(reason:) = ...
end
```

This generates `publish_later` and `retract_later` automatically.

## Testing

Mirror the `app/models` path in tests:
```ruby
# test/models/post/publisher_test.rb
class Post::PublisherTest < ActiveSupport::TestCase
  setup { @publisher = posts(:one).publisher }

  test "publish updates the post" do
    @publisher.publish
    assert @publisher.post.reload.published?
  end
end
```

## Use `record` for polymorphic shared logic

When writing shared modules across multiple Associated Objects,
use `record` instead of the model-specific reader so the module works across types:
```ruby
def price_set? = record.price_cents.positive?
```

## What not to do

- Do not create Associated Objects for trivial CRUD — plain model methods are fine.
- Do not use `app/services` when an Associated Object would give better organization.
- Do not put workflow logic directly in model callbacks — forward to the associated object instead.
- Do not define a wrapping `ActiveSupport::Concern` when `extension` inside the Associated Object is cleaner.