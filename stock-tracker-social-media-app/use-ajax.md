# Use Ajax

#### Update the form submission code to submit the request via ajax:

```text
<%= form_tag search_stocks_path, remote: true, method: :get, id: "stock-lookup-form" do %>
```

#### Also update the code right under it to render the result partial:

```markup
<div id="results">
  <%= render 'users/result' %>
</div>
```

#### If using Rails 5 and following the video exactly:

```markup
<div id="results">
  <%= render 'result' %>
</div>
```

#### Create a new partial under app/views/users folder and call it `_result.html.erb` and move the code from that part of the my\_portfolio page and paste it there:

```markup
<% if @stock %>
  <div class="well results-block">
    <strong>Symbol: </strong> <%= @stock.ticker %>
    <strong>Name: </strong> <%= @stock.name %>
    <strong>Price: </strong> <%= @stock.last_price %>
  </div>
<% end %>
```

#### Now Rails 4 \(Rails 5 follows after this\): Update the search action in the stocks controller file to render this partial

```ruby
def search
  if params[:stock].present?
    @stock = Stock.new_from_lookup(params[:stock])
    if @stock
      render partial: 'users/result'
    else
      flash[:danger] = "You have entered an incorrect symbol"
      redirect_to my_portfolio_path
    end
  else
    flash[:danger] = "You have entered an empty search string"
    redirect_to my_portfolio_path
  end
end
```

#### Add some js code to application.js file under app/assets/javascripts folder to handle the result and send it back to the browser:

```javascript
$(document).ready(function(){
  $('#stock-lookup-form').on('ajax:complete', function(event, data, status){
    $('#results').html(data.responseText)
  })
})
```

#### Now Rails 5 of the same thing \(from updating the search action above\): Update the stocks controller:

```ruby
def search
  if params[:stock].present?
    @stock = Stock.new_from_lookup(params[:stock])
    if @stock
      respond_to do |format|
        format.js { render partial: 'users/result' }
      end
    else
      flash[:danger] = "You have entered an incorrect symbol"
      redirect_to my_portfolio_path
    end
  else
    flash[:danger] = "You have entered an empty search string"
    redirect_to my_portfolio_path
  end
end
```

#### Create a new js partial, `_result.js.erb` under the app/views/users folder and fill it in:

`$('#results').html("<%= j (render 'users/result.html') %>")`

