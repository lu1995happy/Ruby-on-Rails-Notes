# Integration Test and Feature: Listing Categories

## Under `test/integration` folder create a file named `list_categories_test.rb` and fill it in

```ruby
require 'test_helper'

class ListCategoriesTest < ActionDispatch::IntegrationTest

  def setup
    @category = Category.create(name: "sports")
    @category2 = Category.create(name: "programming")
  end

  test "should show categories listing" do
    get categories_path
    assert_template 'categories/index'
    assert_select "a[href=?]", category_path(@category), text: @category.name
    assert_select "a[href=?]", category_path(@category2), text: @category2.name
  end
  
end
```

## Add pagination to the `app/views/categories/index.html.erb` file and make it look like below

```markup
<h1 align="center">Listing All Categories</h1>
<div align="center">
  <%= will_paginate %>
  <% @categories.each do |category| %>
    <ul class="listing">
      <div class="row">
        <div class="well col-md-4 col-md-offset-4">
          <li class="article-title">
            <%= link_to "#{category.name}", category_path(category) %>
          </li>
        </div>
      </div>
    </ul>
  <% end %>
  <%= will_paginate %>
</div>
```

## Update the index action in the `categories_controller.rb` file to accomodate pagination

```ruby
def index
    @categories = Category.paginate(page: params[:page], per_page: 5)
end
```

