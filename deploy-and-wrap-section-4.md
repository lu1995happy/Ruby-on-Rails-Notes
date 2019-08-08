# Deploy and Wrap Section 4

#### Completed articles controller after adding before\_action:

```ruby
class ArticlesController < ApplicationController

    before_action :set_article, only: [:edit, :update, :show, :destroy]
    
    def index
        @articles = Article.all
    end
    
    def new
        @article = Article.new
    end
    
    def edit
    
    end
    
    def create
        @article = Article.new(article_params)
        if @article.save
            flash[:notice] = "Article was successfully created"
            redirect_to article_path(@article)
        else
            render 'new'
        end
    end
    
    def update
        if @article.update(article_params)
            flash[:notice] = "Article was successfully updated"
            redirect_to article_path(@article)
        else
            render 'edit'
        end
    end
    
    def show
    
    end
    
    def destroy
        @article.destroy
        flash[:notice] = "Article was successfully deleted"
        redirect_to articles_path
    end
    
    private
        def set_article
            @article = Article.find(params[:id])
        end
        def article_params
            params.require(:article).permit(:title, :description)
        end
end
```

#### To deploy app to production -&gt;

* Ensure you committed your code to your git repo
* Ensure your gemfile has sqlite3 in group dev and pg and rails\_12factor in group production, if using Rails 5, then you only need gem 'pg', '~&gt; 0.11' in group production \(rails\_12factor is not necessary\)
* Command to deploy to heroku: `git push heroku master`
* Once deployed run the following to run your migration files in production: `heroku run rake db:migrate`, if using Rails 5, `heroku run rails db:migrate`

