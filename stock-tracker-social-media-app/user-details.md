# User Details

#### First generate the migration file:

`rails generate migration add_first_and_last_name_to_users`

#### Pull up the migration file created and add the columns:

```ruby
def change
  add_column :users, :first_name, :string
  add_column :users, :last_name, :string
end
```

#### Run the migration:

`rake db:migrate` 

Rails 5-&gt; `rails db:migrate`

#### Add the method to return full name in the `user.rb` model file:

```ruby
def full_name
  return "#{first_name} #{last_name}".strip if (first_name || last_name)
  "Anonymous"
end
```

#### Update the registrations views to add these fields when users are signing up or editing their accounts, go to `app/views/devise/registrations/new.html.erb` and `edit.html.erb`. Add these fields in right under email:

```markup
<div class="form-group">
  <div class="col-md-6 no-padding">
    <%= f.label :first_name %>
    <%= f.text_field :first_name, class: 'form-control' %>          
  </div>
  <div class="col-md-6 no-padding left-padding">
    <%= f.label :last_name %>
    <%= f.text_field :last_name, class: 'form-control' %>
  </div>
</div>
```

#### Add in the styling in `application.css.scss`:

```css
.no-padding {
  padding: 0 !important;
}

.left-padding {
  padding-left: 15px !important;
}
```

#### Now we need to create a new folder under app/controllers and call in user, within it create a `registrations_controller.rb` file and fill it in:

```ruby
class User::RegistrationsController < Devise::RegistrationsController
  before_action :configure_permitted_parameters
  
  protected
  
    def configure_permitted_parameters
      devise_parameter_sanitizer.permit(:sign_up, keys: [:first_name, :last_name])
      devise_parameter_sanitizer.permit(:account_update, keys: [:first_name, :last_name])
    end
  
end
```

#### Update the `config/routes.rb` file for devise\_for :users

`devise_for :users, :controllers => { :registrations => "user/registrations" }`

