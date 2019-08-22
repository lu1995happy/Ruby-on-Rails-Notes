# Many to Many Associations

#### First generate the association

`rails generate model UserStock user:references stock:references`

#### Run the migration:

Rails 4: `rake db:migrate`

Rails 5: `rails db:migrate`

#### Add the association code in the `stock.rb` model file:

`has_many :user_stocks`

`has_many :users, through: :user_stocks`

#### In the `user.rb` model file:

`has_many :user_stocks`

`has_many :stocks, through: :user_stocks`

#### Update the `_result.html.erb` partial under app/views/users folder and add the route to add the stock to the portfolio of the user after the display of price:

```ruby
<%= link_to "Add to my stocks", user_stocks_path(user: current_user,
                                stock_ticker: @stock.ticker),
                                class: "btn btn-xs btn-success",
                                method: :post %>
```

#### Add the route in the `config/routes.rb` file

`resources :user_stocks, only: [:create]`

#### Now add the controller:

`rails generate controller UserStocks`

#### Then add the create action within it:

```ruby
def create
    stock = Stock.find_by_ticker(params[:stock_ticker])
    if stock.blank?
      stock = Stock.new_from_lookup(params[:stock_ticker])
      stock.save
    end
    @user_stock = UserStock.create(user: current_user, stock: stock)
    flash[:success] = "Stock #{@user_stock.stock.name} was successfully added to portfolio"
    redirect_to my_portfolio_path
  end
```

#### Add the find\_by\_ticker method in the `stock.rb` model file:

```ruby
def self.find_by_ticker(ticker_symbol)
    where(ticker: ticker_symbol).first
end
```

