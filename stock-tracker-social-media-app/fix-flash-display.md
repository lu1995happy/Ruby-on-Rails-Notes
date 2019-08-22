# Fix Flash display

#### To fix the double flash display, go to `_result.html.erb` and surround the flash div in an if condition as below:

```ruby
<% if params[:action] == 'search' %>
  <div class="results-block">
    <%= bootstrap_flash %>
  </div>
<% end %>
```

