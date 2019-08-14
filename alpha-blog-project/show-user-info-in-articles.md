# Show User Info in Articles

#### Add the following code to the index.html.erb file under app/views/articles folder within the div for article-body and under the article.description:

```markup
<div class="article-meta-details">
    <small>Created by: <%= article.user.username if article.user%>,
    <%= time_ago_in_words(article.created_at) %> ago,
    last updated: <%= time_ago_in_words(article.updated_at) %> ago</small>
</div>
```

#### And then add styling to a new article-meta-details class in the custom.css.scss page under the app/assets/stylesheets folder:

```css
.article-meta-details {
    border-top: 1px solid #eaeaea;
    margin-top: 15px;
}
```

