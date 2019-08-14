# Add User Validations

#### Validations for User class:

* username must be present and unique
* email must be present and unique
* validate email format using regex

#### user.rb model file after validations added:

```ruby
class User < ApplicationRecord
  validates :username, presence: true,
            uniqueness: { case_sensitive: false },
            length: { minimum: 3, maximum: 25 }
  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
  validates :email, presence: true, length: { maximum: 105 },
            uniqueness: { case_sensitive: false },
            format: { with: VALID_EMAIL_REGEX }
end
```

