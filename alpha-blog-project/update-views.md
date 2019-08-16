# Update Views

### Add in the following code under description and above article-actions in the `show.html.erb` file under `app/views/articles`folder

```ruby
<% if @article.categories.any? %>
    <p>Categories: <%= render @article.categories %></p>
<% end %>
```

### Under `app/views/categories` folder add a `_category.html.erb` partial and fill it in with the following

```ruby
<span class="badge">
  <%= link_to category.name, category_path(category) %> &nbsp;
</span>
```

### Update styling in your `custom.css.scss` file under `app/assets` directory

```css
.badge {
  background-color: #CEF6F5;
  text-transform: uppercase;
  letter-spacing: -1px;
  font-weight: bold;
}

.input_checkbox input {
  width: auto !important;
}
```

### Next update the `_article.html.erb` partial under the `app/views/articles` folder above the if logged in block for article-actions

```ruby
<% if article.categories.any? %>
    <p>Categories: <%= render article.categories %></p>
<% end %>
```

### Update the `show.html.erb` template under the `app/views/categories` folder

```markup
<h1 align="center"><%= "Category: " + @category.name %></h1>
<div align="center">
  <%= will_paginate @category_articles %>
</div>
<%= render 'articles/article', obj: @category_articles %>
  <div align="center">
<%= will_paginate @category_articles %>
</div>
```

### Update the `categories_controller.rb` file show action

```ruby
def show
  @category = Category.find(params[:id])
  @category_articles = @category.articles.paginate(page: params[:page], per_page: 5)
end
```

### Update the `index.html.erb` page under `app/views/categories` folder to add number of articles in each category

```markup
<h1 align="center">Listing All Categories</h1>
<div align="center">
  <%= will_paginate %>
  <% @categories.each do |category| %>
    <ul class="listing">
      <div class="row">
        <div class="well col-md-4 col-md-offset-4">
          <li class="article-title">
            <%= link_to "#{category.name}", category_path(category) %>
          </li>
          <li>
            <small>
              <%= pluralize(category.articles.count, "article") %>
            </small>
          </li>
        </div>
      </div>
    </ul>
  <% end %>
  <%= will_paginate %>
</div>
```

