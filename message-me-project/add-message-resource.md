# Add message resource

## `app/models/message.rb`

```ruby
class Message < ApplicationRecord
  belongs_to :user
  validates :body, presence: true
end
```

## `app/models/user.rb`

```ruby
class User < ApplicationRecord
  validates :username, presence: true, length: { minimum: 3, maximum: 15 },
            uniqueness: { case_sensitive: false }
  has_many :messages
  has_secure_password
end
```

## `db/migrate/create_message.rb`

```ruby
class CreateMessages < ActiveRecord::Migration[5.2]
  def change
    create_table :messages do |t|
      t.text :body
      t.integer :user_id
      t.timestamps
    end
  end
end
```

