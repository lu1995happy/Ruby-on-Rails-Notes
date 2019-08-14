# New User Signup

#### To add the route for the new form add the following two lines to the routes.rb file:

```ruby
get 'signup', to: 'users#new'
resources :users, except: [:new]
```

#### Create a file under app/controllers folder called users\_controller.rb and fill in the following:

```ruby
class UsersController < ApplicationController
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

  private
    def user_params
      params.require(:user).permit(:username, :email, :password)
    end
end
```

#### To create a view, first create a folder called users under the app/views directory, then within it create a new file called new.html.erb and fill in the following code:

```markup
<h1 align="center">Signup for Alpha Blog</h1>
<%= render 'shared/errors', obj: @user %>
  <div class='row'>
    <div class='col-xs-12'>
    <%= form_for(@user, :html => {class: "form-horizontal", role: "form"}) do |f| %>
      <div class="form-group">
        <div class="control-label col-sm-2">
          <%= f.label :username %>
        </div>
        <div class="col-sm-8">
          <%= f.text_field :username, class: "form-control", placeholder: "Enter username", autofocus: true %>
        </div>
      </div>
      <div class="form-group">
        <div class="control-label col-sm-2">
          <%= f.label :email %>
        </div>
        <div class="col-sm-8">
          <%= f.email_field :email, class: "form-control", placeholder: "Enter email" %>
        </div>
      </div>
      <div class="form-group">
        <div class="control-label col-sm-2">
          <%= f.label :password %>
        </div>
        <div class="col-sm-8">
          <%= f.password_field :password, class: "form-control", placeholder: "Enter password" %>
        </div>
      </div>
      <div class="form-group">
        <div class="col-sm-offset-2 col-sm-10">
          <%= f.submit "Sign up", class: 'btn btn-primary btn-lg' %>
        </div>
      </div>
    <% end %>
    <div class="col-xs-4 col-xs-offset-4">
      [ <%= link_to "Cancel request and return to articles listing", articles_path %> ]
    </div>
  </div>
</div>
```

#### Now test out signing up a couple of users from the UI \(sign up a couple of invalid ones too to ensure the validations are working and displaying correctly\)

#### Then you can test them out from the rails console

