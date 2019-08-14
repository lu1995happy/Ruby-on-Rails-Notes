# Add Users Index

#### First in the users\_controller.rb file add the following index action:

```ruby
def index
   @users = User.all
 end
```

#### Create a file named index.html.erb under the app/views/users folder and fill it in with the following:

```markup
<h1 align="center">All Alpha Bloggers</h1>
<div align="center">
  <% @users.each do |user| %>
    <ul class="listing">
      <div class="row">
        <div class="well col-md-4 col-md-offset-4">
          <li><%= link_to gravatar_for(user), user_path(user) %></li>
          <li class="article-title">
            <%= link_to user.username, user_path(user) %>
          </li>
          <li>
            <small>
              <%= pluralize(user.articles.count, "article") if user.articles %>
            </small>
          </li>
        </div>
      </div>
    </ul>
  <% end %>
</div>
```

#### Add the following class to the custom.css.scss file:

```css
.listing {
    list-style: none;
    padding-left: 0;
}
```

#### Update the show.html.erb file under the app/views/articles folder and add the following bit of code:

```markup
<% if @article.user %>
  <ul class="listing">
    <div class="row center">
      <div class="col-md-4 col-md-offset-4">
        <li>Created by:</li>
        <li><%= link_to gravatar_for(@article.user), user_path(@article.user) %></li>
        <li class="article-title">
          <%= link_to @article.user.username, user_path(@article.user) %>
        </li>
        <li>
          <small>
            <%= pluralize(@article.user.articles.count, "article") if @article.user.articles %>
          </small>
        </li>
      </div>
    </div>
  </ul>
<% end %>
```

#### After addition of the code above, the show.html.erb file in the app/views/articles folder should look like below:

```markup
<h2 align="center">
  Title: <%= @article.title %>
</h2>
<div class="well col-xs-8 col-xs-offset-2">
  <% if @article.user %>
    <ul class="listing">
      <div class="row center">
        <div class="col-md-4 col-md-offset-4">
          <li>Created by:</li>
          <li><%= link_to gravatar_for(@article.user), user_path(@article.user) %></li>
          <li class="article-title">
            <%= link_to @article.user.username, user_path(@article.user) %>
          </li>
          <li>
            <small>
              <%= pluralize(@article.user.articles.count, "article") if @article.user.articles %>
            </small>
          </li>
        </div>
      </div>
    </ul>
  <% end %>
  <h4 class="center description">
    <strong>Description:</strong>
  </h4>
  <hr>
  <%= simple_format(@article.description) %>
  <div class="article-actions">
    <%= link_to "Edit this article", edit_article_path(@article), class: "btn btn-xs btn-primary" %>
    <%= link_to "Delete this article", article_path(@article), method: :delete,
        data: { confirm: "Are you sure you want to delete the article?"},
        class: "btn btn-xs btn-danger" %>
    <%= link_to "View all articles", articles_path, class: "btn btn-xs btn-success" %>
  </div>
</div>
```

