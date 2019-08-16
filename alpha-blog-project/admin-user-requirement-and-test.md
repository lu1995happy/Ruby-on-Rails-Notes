# Admin User Requirement and Test

## Update categories\_controller\_test.rb file to create admin user and then simulate log in

```ruby
require 'test_helper'

class CategoriesControllerTest < ActionDispatch::IntegrationTest
  # (if Rails 4 -> class CategoriesControllerTest < ActionController::TestCase)

  def setup
    @category = Category.create(name: "Sports")
    @user = User.create(username: "john", email: "john@example.com", password: "password", admin: true)
  end

  test "should get categories index" do
    get categories_path
    # (if Rails 4 -> get :index)
    assert_response :success
  end

  test "should get new" do
    sign_in_as(@user, "password")
    get new_category_path
    # (if Rails 4 -> session[:user_id] = @user.id)
    # (if Rails 4 -> get :new)
    assert_response :success
  end

  test "should get show" do
    get category_path(@category)
    # (if Rails 4 -> get(:show, {'id' => @category.id}))
    assert_response :success
  end

  test "should redirect create when admin not logged in" do
    assert_no_difference 'Category.count' do
      post categories_path, params: { category: { name: "sports" } }
      # (if Rails 4 -> post :create, category: { name: "sports" })
    end
    assert_redirected_to categories_path
  end

end
```

### Continuing with Rails 5 specific directions, in the test\_helper.rb file you'll need to add sign\_in\_as method as follows 

```ruby
def sign_in_as(user, password)
  post login_path, params: { session: { email: user.email, password: password } }
end
```

## Add code to require logged in admin users to categories\_controller.rb file:

```ruby
class CategoriesController < ApplicationController

  before_action :require_admin, except: [:index, :show]

  def index
    @categories = Category.paginate(page: params[:page], per_page: 5)
  end

  def new
    @category = Category.new
  end

  def create
    @category = Category.new(category_params)
    if @category.save
      flash[:success] = "Category was created successfully"
      redirect_to categories_path
    else
      render 'new'
    end
  end

  def show

  end

  private
    def category_params
      params.require(:category).permit(:name)
    end

    def require_admin
      if !logged_in? || (logged_in? and !current_user.admin?)
        flash[:danger] = "Only admins can perform that action"
        redirect_to categories_path
      end
    end
    
end
```

