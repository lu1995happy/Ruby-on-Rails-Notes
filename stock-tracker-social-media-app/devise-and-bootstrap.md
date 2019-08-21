# Devise and Bootstrap

#### In your gemfile, add the devise gem:

`gem 'devise'`

#### Then run:

`bundle install --without production`

#### Then install devise in your application:

`rails generate devise:install`

`rails generate devise User`

`rake db:migrate` to add users table

#### Add the following line to the `application_controller.rb` file under app/controllers:

`before_action :authenticate_user!`

#### Add a logout link to the homepage which is the `index.html.erb` view under app/views/welcome folder:

`<%= link_to "logout", destroy_user_session_path, method: :delete %>`

#### Add gem `'twitter-bootstrap-rails'` in your gemfile and bundle install --without production

#### If using Rails 5, also add gem `'jquery-rails'` under gem 'twitter-bootstrap-rails', then run bundle install

#### Then run the following commands:

`rails generate bootstrap:install static`

`rails g bootstrap:layout application`

#### override using Y

#### Then add gem `'devise-bootstrap-views'` in your gemfile and bundle install --without production

#### Under your app/assets/stylesheets folder, add the following line to your application.css file above the \*= require\_tree . line:

`*= require devise_bootstrap_views`

#### If using Rails 5, go over to your app/assets/javascripts/application.js file and add the following two lines under the line that say //= require rails-ujs

`//= require jquery  
//= require twitter/bootstrap`

#### Then run the following two commands from the terminal

`rails g devise:views:locale en`

`rails g devise:views:bootstrap_templates`

#### In your config/routes.rb file add the following line \(it should already exist, confirm that it's there\):

`devise_for :users`

#### Test out in your local, if you are using Rails 5 and you get an error when you preview that is complaining about favicon assets not being present, you can simply remove these lines from your app/views/layouts/application.html.erb \(usually between lines 14 and 30\) that reference favicon\_link\_tags, there are usually 5

