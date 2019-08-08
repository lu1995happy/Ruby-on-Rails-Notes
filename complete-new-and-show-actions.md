# Complete New and Show Actions

## Complete New and Show Actions

#### Completed create action in articles controller:

```ruby
def create
    @article = Article.new(article_params)
    if @article.save
        flash[:notice] = "Article was successfully created"
        redirect_to article_path(@article)
    else
        render 'new'
    end
end
```

#### Flash message code added to application.html.erb under app/views/layouts folder \(right under &lt;body&gt; and above &lt;%= yield %&gt;:

```ruby
<% flash.each do |name, msg| %>
    <ul>
        <li><%= msg %></li>
    </ul>
<% end %>
```

#### Code added to display errors in the new.html.erb template under app/views/articles folder:

```ruby
<% if @article.errors.any? %>
    <h2>The following errors prevented the article from getting created</h2>
    <ul>
        <% @article.errors.full_messages.each do |msg| %>
            <li><%= msg %></li>
        <% end %>
    </ul>
<% end %>
```

#### To create the show action, add the following show method to articles\_controller.rb file:

```ruby
def show
    @article = Article.find(params[:id])
end
```

#### To create the show view, add a show.html.erb file under the app/views/articles folder and fill in the code:

```ruby
<h1>Showing selected article</h1>
<p>
    Title: <%= @article.title %>
</p>
<p>
    Description: <%= @article.description %>
</p>
```

