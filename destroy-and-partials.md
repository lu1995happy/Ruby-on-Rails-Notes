# Destroy and Partials

#### Add this link to the homepage \(root route\) so you can access the blog from the homepage:

`<%= link_to "Alpha Blog", articles_path %>`

#### Under app/views/layouts folder create a \_messages.html.erb file \(messages partial\) and remove the following code from application.html.erb to this file:

```ruby
<% flash.each do |name, msg| %>
    <ul>
        <li><%= msg %></li>
    </ul>
<% end %>
```

#### In place of this code in the application.html.erb add the following code:

`<%= render 'layouts/messages' %>`

#### Create a file under app/views/articles folder called \_form.html.erb and fill it in with the following code \(copied from the new or edit.html.erb page\):

```ruby
<% if @article.errors.any? %>
    <h2>The following errors prevented the article from getting created</h2>
    <ul>
        <% @article.errors.full_messages.each do |msg| %>
            <li><%= msg %></li>
        <% end %>
    </ul>
<% end %>

<%= form_for @article do |f| %>
    <p>
        <%= f.label :title %><br/>
        <%= f.text_field :title %>
    </p>
    <p>
        <%= f.label :description %><br/>
        <%= f.text_area :description %>
    </p>
    <p>
        <%= f.submit %>
    </p>
<% end %>

<%= link_to "Back to articles listing", articles_path %>
```

#### Then remove the code above from both new.html.erb and edit.html.erb files and in it's place add the following code:

`<%= render 'form' %>`

#### To add the destroy method, first add the following to the articles controller:

```ruby
def destroy
    @article = Article.find(params[:id])
    @article.destroy
    flash[:notice] = "Article was successfully deleted"
    redirect_to articles_path
end
```

#### Then in the index.html.erb \(listings page\) add the following link as one of the &lt;td&gt; items under the show article link:

`<td><%= link_to 'Delete', article_path(article), method: :delete, data: {confirm: "Are you sure?"} %></td>`

