# Build Stock Lookup Form

## `my_portfolio.html.erb page`

```markup
<h1>My Portfolio</h1>
<h3>Search for Stocks</h3>
<div id="stock-lookup">
  <%= form_tag "#", method: :get, id: "stock-lookup-form" do %>
    <div class="form-group row no-padding text-center col-md-12">
      <div class="col-md-10">
        <%= text_field_tag :stock, params[:stock],
                                  placeholder: "Stock ticker symbol", autofocus: true,
                                  class: "form-control search-box input-lg" %>
      </div>
      <div class="col-md-2">
        <%= button_tag(type: :submit, class: "btn btn-lg btn-success") do %>
          <i class="fa fa-search"></i> Look up a stock
        <% end %>
      </div>
    </div>
  <% end %>
</div>
```
