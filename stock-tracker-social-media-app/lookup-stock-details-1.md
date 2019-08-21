# Lookup Stock Details

#### Add the route for search\_stocks in `config/routes.rb` file:

`get 'search_stocks', to: 'stocks#search'`

#### Now you have to build the `stocks_controller.rb` file under app/controllers and fill it in:

```ruby
class StocksController < ApplicationController
  
  def search
    @stock = Stock.new_from_lookup(params[:stock])
    render 'users/my_portfolio'
  end

end
```

#### Update the form code in your my\_portfolio view for stocks by changing the form\_tag line to look like below:

`<%= form_tag search_stocks_path, method: :get, id: "stock-lookup-form" do %>`

#### Add the new\_from\_lookup and strip\_commas methods in your stock model to perform the search:

```ruby
def self.new_from_lookup(ticker_symbol)
  looked_up_stock = StockQuote::Stock.quote(ticker_symbol)
  price = strip_commas(looked_up_stock.l)
  new(name: looked_up_stock.name, ticker: looked_up_stock.symbol, last_price: price)
end

def self.strip_commas(number)
  number.gsub(",", "")
end
```

#### In your my\_portfolio at the bottom of the page add some code to display the results block:

```markup
<div class="well results-block">
  <strong>Symbol: </strong> <%= @stock.ticker %>
  <strong>Name: </strong> <%= @stock.name %>
  <strong>Price: </strong> <%= @stock.last_price %>
</div>
```

#### Add some styling, go to `app/assets/application.css` file \(rename it to application.css.scss\):

```css
.results-block {
  display: inline-block;
}

.no-padding {
  padding: 0 !important;
}
```

