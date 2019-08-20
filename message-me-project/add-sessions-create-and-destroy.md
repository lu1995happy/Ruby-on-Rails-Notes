# Add sessions create and destroy

## `sessions_controller.rb`

```ruby
class SessionsController < ApplicationController

   def create
    user = User.find_by(username: params[:session][:username])
    if user && user.authenticate(params[:session][:password])
      session[:user_id] = user.id
      flash[:success] = "You have successfully logged in"
      redirect_to root_path
    else
      flash.now[:error] = "There was something wrong with your login information"
      render 'new'
    end
   end

   def destroy
    session[:user_id] = nil
    flash[:success] = "You have successfully logged out"
    redirect_to login_path
   end	

end
```

## `_navigation.html.erb`

```markup
<div class="right menu">
  <div class="ui dropdown item">
    Account <i class="dropdown icon"></i>
    <div class="menu">
      <% if logged_in? %>
        <%= link_to "Logout", logout_path, method: :delete, class: "item" %>
      <% else %>
        <%= link_to "Log in", login_path, class: "item" %>
      <% end %>
    </div>
  </div>
  <% if !logged_in? %>
    <div class="item">
      <%= link_to "Log in", login_path, class: "ui primary button" %>
    </div>
  <% end %>
</div>
```

## `routes.rb`

```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
  root 'chatroom#index'
  get 'login', to: 'sessions#new'
  post 'login', to: 'sessions#create'
  delete 'logout', to: 'sessions#destroy'
end
```

