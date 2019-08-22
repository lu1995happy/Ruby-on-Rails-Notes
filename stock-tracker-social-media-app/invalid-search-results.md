# Invalid Search Results

#### Update the search method in stocks\_controller to deal with empty & incorrect search strings:

```ruby
class StocksController < ApplicationController

  def search
    if params[:stock].present?
      @stock = Stock.new_from_lookup(params[:stock])
      if @stock
        render 'users/my_portfolio'
      else
        flash[:danger] = "You have entered an incorrect symbol"
        redirect_to my_portfolio_path
      end
    else
      flash[:danger] = "You have entered an empty search string"
      redirect_to my_portfolio_path
    end
  end

end
```

#### Then in my\_portfolio.html.erb add the display for results in an if block to look for @stock

```markup
<% if @stock %>
  <div class="well results-block">
    <strong>Symbol: </strong> <%= @stock.ticker %>
    <strong>Name: </strong> <%= @stock.name %>
    <strong>Price: </strong> <%= @stock.last_price %>
  </div>
<% end %>
```

#### Update new\_from\_lookup method to deal with exception scenario:

```ruby
def self.new_from_lookup(ticker_symbol)
  begin
    looked_up_stock = StockQuote::Stock.quote(ticker_symbol)
    price = strip_commas(looked_up_stock.l)
    new(name: looked_up_stock.name, ticker: looked_up_stock.symbol, last_price: price)
  rescue Exception => e
    return nil
  end
end
```

