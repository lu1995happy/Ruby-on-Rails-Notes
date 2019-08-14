# Edit Users

#### First add the following two actions in the users\_controller.rb file:

```ruby
def edit
  @user = User.find(params[:id])
end

def update
  @user = User.find(params[:id])
  if @user.update(user_params)
    flash[:success] = "Your account was updated successfully"
    redirect_to articles_path
  else
    render 'edit'
  end
end
```

#### Then create a \_form.html.erb form partial file under the app/views/users folder and fill it in with the following code:

```markup
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

#### The updated new.html.erb file under app/views/users folder should look like below:

```markup
<h1 align="center">Edit your account</h1>
<%= render 'form' %>
```

#### Create a new file under app/views/users called edit.html.erb and fill it in with the following code:

```markup
<h1 align="center">Edit your account</h1>
<%= render 'form' %>
```

#### Test out creating and editing a couple of users from the browser

