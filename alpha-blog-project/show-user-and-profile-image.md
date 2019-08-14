# Show User and Profile Image

#### To have a profile image associated with an email account you control, add one to the site en.gravatar.com. This will be the globally recognized avatar \(gravatar for short\) associated with that email address.

#### In the users\_controller.rb file add in the following method:

```ruby
def show
   @user = User.find(params[:id])
 end
```

#### In the application\_helper.rb file under the app/helpers folder, add the following method:

```ruby
def gravatar_for(user, options = { size: 80})
    gravatar_id = Digest::MD5::hexdigest(user.email.downcase)
    size = options[:size]
    gravatar_url = "https://secure.gravatar.com/avatar/#{gravatar_id}?s=#{size}"
    image_tag(gravatar_url, alt: user.username, class: "img-circle")
end
```

#### Under the app/views/articles folder, create a file called \_article.html.erb and fill it in with the following code:

```markup
<% obj.each do |article| %>
  <div class="row">
    <div class="col-xs-8 col-xs-offset-2">
      <div class="well well-lg">
        <div class="article-title">
          <%= link_to article.title, article_path(article) %>
        </div>
        <div class="article-body">
          <%= truncate(article.description, length: 100) %>
          <div class="article-meta-details">
            <small>Created by: <%= article.user.username if article.user%>,
            <%= time_ago_in_words(article.created_at) %> ago,
            last updated: <%= time_ago_in_words(article.updated_at) %> ago</small>
          </div>
        </div>
        <div class="article-actions">
          <%= link_to "Edit this article", edit_article_path(article), class: "btn btn-xs btn-primary" %>
          <%= link_to "Delete this article", article_path(article), method: :delete,
              data: { confirm: "Are you sure you want to delete the article?"},
              class: "btn btn-xs btn-danger" %>
        </div>
      </div>
    </div>
  </div>
<% end %>
```

#### Change the index.html.erb file under the app/views/articles folder to look like below:

```markup
<h1 align="center">Listing all articles</h1>
<%= render 'article', obj: @articles %>
```

#### Create a new file named show.html.erb under the app/views/users folder and fill in the following code:

```markup
<h1 align="center">Welcome to <%= @user.username %>'s page</h1>
<div class="row">
  <div class="col-md-4 col-md-offset-4 center">
    <%= gravatar_for @user, size: 150 %>
  </div>
</div>
<h4 align="center"><%= @user.username %>'s articles</h4>
<%= render 'articles/article', obj: @user.articles %>
```

