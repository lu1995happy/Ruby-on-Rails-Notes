# Stocks Listing and Remove

#### First go to `my_portfolio.html.erb` file and render a partial at the bottom

`<%= render 'stocks/list' %>`

#### Then create a new folder called stocks under app/views then under the stocks folder create a new file called `_list.html.erb` then fill in the code to display the stocks:

```markup
<table class="table table-striped">
  <thead>
    <tr>
      <th>Name</th>
      <th>Symbol</th>
      <th>Current Price</th>
      <% if @user.id == current_user.id %>
        <th>Actions</th>
      <% end %>
    </tr>
  </thead>
  <tbody>
    <% @user_stocks.each do |user_stock| %>
      <tr>
        <td><%= user_stock.name %></td>
        <td><%= user_stock.ticker %></td>
        <td><%= user_stock.last_price %></td>
        <% if @user.id == current_user.id %>
          <td>
            <%= link_to "Delete this stock", user_stock_path(user_stock), 
                      method: :delete,
                      data: {confirm: "Are you sure?"}, 
                      class: "btn btn-xs btn-danger" %>
          </td>
        <% end %>
      </tr>
    <% end %>
  </tbody>
</table>
```

#### Go to the users\_controller and my\_portfolio action and grab the two instance variables necessary:

```ruby
def my_portfolio
  @user = current_user
  @user_stocks = current_user.stocks
end
```

#### Go to `config/routes.rb` file and add the destroy route for user\_stocks

`resources :user_stocks, only: [:create, :destroy]`

#### Add the destroy action in the `user_stocks.rb` controller file:

```ruby
def destroy
  stock = Stock.find(params[:id])
  @user_stock = UserStock.where(user_id: current_user.id, stock_id: stock.id).first
  @user_stock.destroy
  flash[:notice] = "Stock was successfully removed from portfolio"
  redirect_to my_portfolio_path
end
```

