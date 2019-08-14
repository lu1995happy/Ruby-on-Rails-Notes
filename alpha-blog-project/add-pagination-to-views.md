# Add Pagination to Views

#### Add the two gems required for pagination to the gemfile:

`gem 'will_paginate', '3.1.5'`

`gem 'bootstrap-will_paginate', '1.0.0'`

#### Then from the command line run:

`bundle install --without production`

#### This will install the gems

#### Change the index action in the articles\_controller.rb file to look like below:

```ruby
def index
    @articles = Article.paginate(page: params[:page], per_page: 5)
end
```

#### Change the index.html.erb page under the app/views/articles folder to look like below:

```markup
<h1 align="center">Listing all articles</h1>
<div align="center">
  <%= will_paginate %>
</div>
<%= render 'article', obj: @articles %>
<div align="center">
  <%= will_paginate %>
</div>
```

#### Change the index action in the users\_controller.rb file to look like below:

```ruby
def index
  @users = User.paginate(page: params[:page], per_page: 5)
end
```

#### Change the show action in the users\_controller.rb file to look like below:

```ruby
def show
  @user = User.find(params[:id])
  @user_articles = @user.articles.paginate(page: params[:page], per_page: 5)
end
```

#### Add the &lt;%= will\_paginate %&gt; line to the index.html.erb view under the app/views/users folder and make it look like below:

```markup
<h1 align="center">All Alpha Bloggers</h1>
<div align="center">
  <%= will_paginate %>
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
  <%= will_paginate %>
</div>
```

#### Change the bottom of the show.html.erb view under the app/views/users folder by adding the pagination and @user\_articles code and make it look like below:

```markup
<h1 align="center">Welcome to <%= @user.username %>'s page</h1>
<div class="row">
  <div class="col-md-4 col-md-offset-4 center">
    <%= gravatar_for @user, size: 150 %>
  </div>
</div>
<h4 align="center"><%= @user.username %>'s articles</h4>
<div class="center">
  <%= will_paginate @user_articles %>
</div>
<%= render 'articles/article', obj: @user_articles %>
<div class="center">
  <%= will_paginate @user_articles %>
</div>
```

