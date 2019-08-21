# Stock Model

#### Remove the sidebar div from the `application.html.erb` file under app/views/layouts folder

#### Remove\(or code out\) the following code for forgot your password link from the `_links.html.erb` partial under the app/views/devise/shared folder:

```markup
<%- if devise_mapping.recoverable? && controller_name != 'passwords' %>
<%= link_to t(".forgot_your_password", :default => "Forgot your password?"), new_password_path(resource_name)
%><br />
<% end -%>
```

#### Generate Stock model:

`rails g model Stock ticker:string name:string last_price:decimal`

#### Create the table by running the migration:

`rake db:migrate`

#### Add gem `'stock_quote'` to your gemfile and run bundle install --without production

**IMPORTANT: Please review the stock\_quote gem documentation in Github as the methods change from time to time**

#### Hop on `rails console` to get stock price for a stock:

`StockQuote::Stock.quote("symbol")`

`StockQuote::Stock.quote("symbol").op`

`StockQuote::Stock.quote("symbol").last_price`

#### Now need to add a view page for my portfolio, we'll call it my portfolio, so go to `config/routes.rb` file and add in the following route:

`get 'my_portfolio', to: 'users#my_portfolio'`

#### Create a `users_controller.rb` file under app/controllers and add in my\_portfolio action:

```ruby
class UsersController < ApplicationController
    def my_portfolio
    end
end
```

#### under views add users folder and under it create a `my_portfolio.html.erb` file and fill it in:

`<h1>My Portfolio</h1>`

#### You may add this as your root route in your `config/routes.rb` file by changing root to `users#my_portfolio`

