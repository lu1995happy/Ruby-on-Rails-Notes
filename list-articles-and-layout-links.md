# List Articles and Layout Links

#### To create listings index first add the index action to acticles controller:

```ruby
def index
    @articles = Article.all
end
```

#### Create the view file index.html.erb under app/views/articles folder:

```ruby
<h1>Listing all articles</h1>
<p>
    <%= link_to "Create new article", new_article_path %>
</p>
<table>
    <tr>
        <th>Title</th>
        <th>Description</th>
    </tr>
    <% @articles.each do |article| %>
        <tr>
            <td><%= article.title %></td>
            <td><%= article.description %></td>
            <td><%= link_to 'Edit', edit_article_path(article) %></td>
            <td><%= link_to 'Show', article_path(article) %></td>
        </tr>
    <% end %>
</table>
```

#### Then update the views with links -&gt; show.html.erb:

```ruby
<h1>Showing selected article</h1>
<p>
    Title: <%= @article.title %>
</p>
<p>
    Description: <%= @article.description %>
</p>
<%= link_to "Edit this article", edit_article_path(@article) %> |
<%= link_to "Back to articles listing", articles_path %>
```

#### Add the back to articles listing path to the bottom of both new.html.erb and edit.html.erb pages:

`<%= link_to "Back to articles listing", articles_path %>`

