# Integration Test for Invalid Category

## Add the following test to `create_categories_test.rb` file under `test/integration` folder

```ruby
test "invalid category submission results in failure" do
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
```

