# Create New Articles from UI

## Create New Articles Command

#### In the config/routes.rb file add the following line to add all the routes for articles:

`resources :articles`

#### This will add the following routes:

routes path HTTP verb link controller\#action

articles index articles GET /articles articles\#index

new article new\_article GET /articles/new articles\#new

create article POST /articles articles\#create

edit article edit\_article GET /articles/:id articles\#edit

update article PATCH /articles/:id articles\#update

show article article GET /articles/:id articles\#show

delete article DELETE /articles/:id articles\#destroy

#### To create articles controller with a new action, under app/controllers create a file named articles\_controller.rb \(snake case\):

```ruby
class ArticlesController < ApplicationController
    def new
        @article = Article.new
    end
end
```

#### To create a view, under app/views create a folder named articles and within it create a file named new.html.erb then fill in the following:

```ruby
<h1>Create an article</h1>

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
```

#### Create action and private article\_params method for string parameters in the articles controller \(Note: This is not complete\):

```ruby
def create
    @article = Article.new(article_params)
    @article.save
    redirect_to article_path(@article)
end

private
    def article_params
        params.require(:article).permit(:title, :description)
    end
```

