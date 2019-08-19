# Update sign in form and add authentication methods

## `application_controller.rb`

```ruby
class ApplicationController < ActionController::Base
  helper_method :current_user, :logged_in?

  def current_user
    @current_user ||= User.find(session[:user_id]) if session[:user_id]
  end

  def logged_in?
    !!current_user
  end

  def require_user
    if !logged_in?
      flash[:error] = "You must be logged in to perform that action"
      redirect_to login_path
    end
  end
end
```

## views/sessions/new.html.erb

```markup
<div class="column">
  <%= form_for(:session, html: {class: "ui form", role: "form"}, url: login_path) do |f| %>
    <div class="field">
      <%= f.label :username, "Username" %>
      <div class="ui left icon input">
        <%= f.text_field :username, placeholder: "Username" %>
        <i class="user icon"></i>
      </div>
    </div>
    <div class="field">
      <%= f.label :password, "Password" %>
      <div class="ui left icon input">
        <%= f.password_field :password, placeholder: "Password" %>
        <i class="lock icon"></i>
      </div>
    </div>
    <%= f.button "Login", class: "ui orange submit button" %>
  <% end %>
</div>
```

