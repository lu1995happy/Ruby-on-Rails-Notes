# Categories Controller and Tests

## Create a file named categories\_controller\_test.rb under the test/controllers folder and fill it in with the following

```ruby
require 'test_helper'

class CategoriesControllerTest < ActionDispatch::IntegrationTest
  # (if Rails 4 -> class CategoriesControllerTest < ActionController::TestCase)

  def setup
    @category = Category.create(name: "sports")
  end

  test "should get categories index" do
    get categories_path
    # (if Rails 4 -> get :index)
    assert_response :success
  end

  test "should get new" do
    get new_category_path
    # (if Rails 4 -> get :new)
    assert_response :success
  end

  test "should get show" do
    get category_path(@category)
    # (if Rails 4 -> get(:show, {'id' => @category.id}))
    assert_response :success
  end

end
```

## Under app/controllers folder create a file named categories\_controller.rb and fill it in:

```ruby
class CategoriesController < ApplicationController

  def index

  end

  def new

  end

  def show

  end

end
```

### In your config/routes.rb file add in the following route for categories:

`resources :categories, except: [:destroy]`

### Under app/views folder create a folder called categories and create 3 files, `new.html.erb`, `index.html.erb` and `show.html.erb`

