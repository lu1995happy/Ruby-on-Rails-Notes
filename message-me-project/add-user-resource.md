# Add user resource

## Gemfile

`gem 'bcrypt', '~> 3.1.7'` 

`gem 'hirb'`

## Command

### create model and migrate file at the same time

`rails generate model User`

### create all users at once

`rails db:seed`

### show all db data in a table

`rails console`

`Hirb.enable`

## `models/user.rb`

```ruby
class User < ApplicationRecord
  validates :username, presence: true, length: { minimum: 3, maximum: 15 }
  has_secure_password
end
```

## `db/migrate/create_user.rb`

```ruby
class CreateUsers < ActiveRecord::Migration[5.2]
  def change
    create_table :users do |t|
      t.string :username
      t.string :password_digest
      t.timestamps
    end
  end
end
```

## `db/seeds.rb`

```ruby
User.create(username: "Evgeny", password: "password")
User.create(username: "Jonsnow", password: "password")
User.create(username: "Arya", password: "password")
User.create(username: "Frodo", password: "password")
User.create(username: "Gandalf", password: "password")
```

