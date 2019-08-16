# Update Tests and Navbar

## Update the `create_categories_test.rb` integration test file under `test/integration` folder to sign in an admin user

```ruby
require 'test_helper'

class CreateCategoriesTest < ActionDispatch::IntegrationTest

  def setup
    @user = User.create(username: "john", email: "john@example.com", password: "password", admin: true)
  end

  test "get new category form and create category" do
    sign_in_as(@user, "password")
    get new_category_path
    assert_template 'categories/new'
    assert_difference 'Category.count', 1 do
      post categories_path, params: { category: { name: "sports" }}
      follow_redirect!
      # if using Rails 4 use below line instead of 2 lines above (without the comment tag of course):
      # categories_path, category: {name: "sports"}
    end
    assert_template 'categories/index'
    assert_match "sports", response.body
  end

  test "invalid category submission results in failure" do
    sign_in_as(@user, "password")
    get new_category_path
    assert_template 'categories/new'
    assert_no_difference 'Category.count' do
      post categories_path, params: { category: {name: " "}}
      # If using Rails 4, use below line instead of above
      # post categories_path, category: {name: " "}
    end
    assert_template 'categories/new'
    assert_select 'h2.panel-title'
    assert_select 'div.panel-body'
  end
end
```

## Add sign\_in\_user method to `test_helper.rb` file under test folder:

```ruby
def sign_in_as(user, password)
    post login_path, params: { session: { email: user.email, password: password } }
    # if (Rails 4 -> post login_path, session: {email: user.email, password: password})
end
```

## Update the navigation partial to display categories including restrictions based on admin user for new categories path by adding the following code right under the &lt;% end %&gt; block for Actions and above the &lt;/ul&gt; tag:

```markup
<li class="dropdown">
  <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Categories <span class="caret"></span></a>
  <ul class="dropdown-menu">
    <li><%= link_to "All Categories", categories_path %></li>
    <% Category.all.each do |category| %>
      <li><%= link_to "#{category.name}", category_path(category) %></li>
    <% end %>
    <% if logged_in? and current_user.admin? %>
      <li role="separator" class="divider"></li>
      <li><%= link_to "Create New Category", new_category_path %></li>
    <% end %>
  </ul>
</li>
```

