# Category Model and Unit Tests

## Create a category\_test.rb file under test/models folder and fill it in with the following

```ruby
require 'test_helper'

class CategoryTest < ActiveSupport::TestCase

  def setup
    @category = Category.new(name: "sports")
  end

  test "category should be valid" do
    assert @category.valid?
  end

  test "name should be present" do
    @category.name = " "
    assert_not @category.valid?
  end

  test "name should be unique" do
    @category.save
    category2 = Category.new(name: "sports")
    assert_not category2.valid?
  end

  test "name should not be too long" do
    @category.name = "a" * 26
    assert_not @category.valid?
  end

  test "name should not be too short" do 
    @category.name = "aa"
    assert_not @category.valid?
  end

end
```

## Create a model file named category.rb under the app/models folder and fill it in

```ruby
class Category < ApplicationRecord
  # (if Rails 4 -> class Category < ActiveRecord::Base)
  validates :name, presence: true, length: { minimum: 3, maximum: 25 }
  validates_uniqueness_of :name
end 
```

#### To create a migration file to create the categories table:

`rails generate migration create_categories`

#### Then fill in the migration file within the create\_table block:

`t.string :name`

`t.timestamps`

#### Run the migration to create the categories table:

`rake db:migrate`

