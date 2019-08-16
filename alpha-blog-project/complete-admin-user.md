# Complete Admin User

## Updated users\_controller.rb file \(several updates\)

```ruby
class UsersController < ApplicationController

  before_action :set_user, only: [:edit, :update, :show]
  before_action :require_same_user, only: [:edit, :update, :destroy]
  before_action :require_admin, only: [:destroy]

  def index
    @users = User.paginate(page: params[:page], per_page: 5)
  end

  def new
    @user = User.new
  end

  def create
    @user = User.new(user_params)
    if @user.save
      session[:user_id] = @user.id
      flash[:success] = "Welcome to the alpha blog #{@user.username}"
      redirect_to user_path(@user)
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

  def destroy
    @user = User.find(params[:id])
    @user.destroy
    flash[:danger] = "User and all articles created by user have been deleted"
    redirect_to users_path
  end

  def set_user
    @user = User.find(params[:id])
  end

  private
    def user_params
      params.require(:user).permit(:username, :email, :password)
    end

    def require_same_user
      if current_user != @user and !current_user.admin?
        flash[:danger] = "You can only edit your own account"
        redirect_to root_path
      end
    end

    def require_admin
      if logged_in? and !current_user.admin?
        flash[:danger] = "Only admin users can perform that action"
        redirect_to root_path
      end
    end
end
```

## Updated user.rb model file under app/models folder

```ruby
class User < ApplicationRecord
  has_many :articles, dependent: :destroy
  before_save { self.email = email.downcase }
  validates :username, presence: true,
            uniqueness: { case_sensitive: false },
            length: { minimum: 3, maximum: 25 }
  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
  validates :email, presence: true, length: { maximum: 105 },
            uniqueness: { case_sensitive: false },
            format: { with: VALID_EMAIL_REGEX }
  has_secure_password
end
```

## Updated index.html.erb file under app/views/users folder

```markup
<h1 align="center">All Alpha Bloggers</h1>
<div align="center">
  <%= will_paginate %>
  <% @users.each do |user| %>
    <ul class="listing">
      <div class="row">
        <div class="well col-md-4 col-md-offset-4">
          <li><%= link_to gravatar_for(user), user_path(user) %></li>
          <li class="article-title">
            <%= link_to user.username, user_path(user) %>
          </li>
          <li>
            <small>
              <%= pluralize(user.articles.count, "article") if user.articles %>
            </small>
          </li>
          <% if logged_in? and current_user.admin? %>
            <li>
              <%= link_to "Delete this user", user_path(user), method: :delete,
                  data: { confirm: "Are you sure you want to delete the user and all their articles?" } %>
            </li>
          <% end %>
        </div>
      </div>
    </ul>
  <% end %>
  <%= will_paginate %>
</div>
```

## To deploy to heroku, ensure you have committed your code to your git repo, then

`git push heroku master`

#### Then run any pending migrations:

`heroku run rake db:migrate`

#### To set admin user from heroku app run:

`heroku run rails console`

#### Then grab a user \(example, user = User.last\):

`user.toggle!(:admin)`

#### That will set the admin column to true \(if it was false\)

