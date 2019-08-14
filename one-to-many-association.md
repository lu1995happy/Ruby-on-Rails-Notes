# One to Many Association

#### To generate a migration to add user\_id column to articles table:

`rails generate migration add_user_id_to_articles`

#### Then within the change method:

`add_column :articles, :user_id, :integer`

#### Then run the migration file to effect the change:

`rake db:migrate`

#### Add the following line to article.rb model file:

`belongs_to :user`

#### Add the following line to user.rb model file:

`has_many :articles`

#### Also add the following line to user.rb model file\(this has nothing to do with the association\):

`before_save { self.email = email.downcase }`

#### Ensure you have a couple of users created by using the rails console. Then add in 1 line to grab a user to the create action to temporarily hardcode a user to articles:

```ruby
def create
    @article = Article.new(article_params)
    @article.user = User.first
    if @article.save
        flash[:success] = "Article was successfully created"
        redirect_to article_path(@article)
    else
        render 'new'
    end
end
```

#### Ensure you get rid of the debugger line if you no londer need it within the create action, you can add that line as you need to your actions if you want to pause execution of a request

#### You can add in the following line to display the debug\(params\) to your development environment UI output:

#### \(this will be in the app/views/layouts/application.html.erb file under render footer and above &lt;/body&gt;\)

`<%= debug(params) if Rails.env.development? %>`

