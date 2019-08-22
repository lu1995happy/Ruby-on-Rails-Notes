# Stock Restrictions

#### Add the 3 methods first in the `user.rb` model file:

```ruby
def stock_already_added?(ticker_symbol)
  stock = Stock.find_by_ticker(ticker_symbol)
  return false unless stock
  user_stocks.where(stock_id: stock.id).exists?
end

def under_stock_limit?
  (user_stocks.count < 10)
end

def can_add_stock?(ticker_symbol)
  under_stock_limit? && !stock_already_added?(ticker_symbol)
end
```

#### Now go to `_result.html.erb` under app/views/users folder and add the restrictions to the view:

```ruby
<% if current_user.can_add_stock?(@stock.ticker) %>
  <%= link_to "Add to my stocks", user_stocks_path(user: current_user,
                                  stock_ticker: @stock.ticker),
                                  class: "btn btn-xs btn-success",
                                  method: :post %>
<% else %>
  <span class="label label-default">
    Stock cannot be added because you have already added
    <% if !current_user.under_stock_limit? %>
      10 stocks
    <% end %>
    <% if current_user.stock_already_added?(@stock.ticker) %>
      this stock
    <% end %>
  </span>
<% end %>
```

