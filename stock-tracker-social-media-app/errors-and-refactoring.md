# Errors and Refactoring

#### Update the `_result.html.erb` partial and add the code to the top:

```markup
<div class="results-block">
  <%= bootstrap_flash %>
</div>
```

#### Update the search actions in the stocks controller and refactor the code 

```ruby
# Rails 4
def search
  if params[:stock].blank? 
    flash.now[:danger] = "You have entered an empty search string"
  else
    @stock = Stock.new_from_lookup(params[:stock])
    flash.now[:danger] = "You have entered an incorrect symbol" unless @stock
  end
  render partial: 'users/result'
end

# Rails 5
def search
  if params[:stock].blank?
    flash.now[:danger] = "You have entered an empty search string"
  else
    @stock = Stock.new_from_lookup(params[:stock])
    flash.now[:danger] = "You have entered an incorrect symbol" unless @stock
  end
  respond_to do |format|
    format.js { render partial: 'users/result' }
  end
end
```

