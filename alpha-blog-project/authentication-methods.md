# Authentication Methods

#### Add the methods and code to make the application\_controller.rb file look like below:

```ruby
class ApplicationController < ActionController::Base
  # Prevent CSRF attacks by raising an exception.
  # For APIs, you may want to use :null_session instead.
  protect_from_forgery with: :exception
  helper_method :current_user, :logged_in?

  def current_user
    @current_user ||= User.find(session[:user_id]) if session[:user_id]
  end

  def logged_in?
    !!current_user
  end

  def require_user
    if !logged_in?
      flash[:danger] = "You must be logged in to perform that action"
      redirect_to root_path
    end
  end
end
```

#### Update the navigation partial where you added the logout link in the last lecture \(last ul class in the view\) and make it look like below:

```markup
<ul class="nav navbar-nav navbar-right">
  <% if logged_in? %>
    <li><%= link_to 'Log out', logout_path, method: :delete %></li>
    <li class="dropdown">
      <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Your Profile<span class="caret"></span></a>
      <ul class="dropdown-menu">
        <li><%= link_to "Edit your profile", edit_user_path(current_user) %></li>
        <li><%= link_to "View your profile", user_path(current_user) %></li>
        <li><a href="#">Something else here</a></li>
        <li role="separator" class="divider"></li>
        <li><a href="#">Separated link</a></li>
      </ul>
    </li>
  <% else %>
    <li><%= link_to 'Log in', login_path %></li>
    <li><%= link_to 'Sign up', signup_path %></li>
  <% end %>
</ul>
```

#### Extract the redundancy from the users\_controller.rb file by using a before\_action :set\_user on top to make the file look like below:

```ruby
class UsersController < ApplicationController

  before_action :set_user, only: [:edit, :update, :show]

  def index
    @users = User.paginate(page: params[:page], per_page: 5)
  end

  def new
    @user = User.new
  end

  def create
    @user = User.new(user_params)
    if @user.save
      flash[:success] = "Welcome to the alpha blog #{@user.username}"
      redirect_to articles_path
    else
      render 'new'
    end
  end

  def edit
  end

  def update
    if @user.update(user_params)
      flash[:success] = "Your account was updated successfully"
      redirect_to articles_path
    else
      render 'edit'
    end
  end

  def show
    @user_articles = @user.articles.paginate(page: params[:page], per_page: 5)
  end

  def set_user
    @user = User.find(params[:id])
  end

  private
    def user_params
      params.require(:user).permit(:username, :email, :password)
    end
end
```

