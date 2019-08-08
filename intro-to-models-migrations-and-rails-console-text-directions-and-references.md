# Intro to Models, Migrations and Rails Console

## Article Table

**Model name**: Article, class: Article -&gt; Capitalized A and singular

**File name**: article.rb -&gt; singular and all lowercase

**Controller file name**: articles\_controller.rb, class: ArticlesController -&gt; camel case class name, snake case file name both plural

**Views folder**: articles

**Table name**: articles -&gt; plural of model

## User Table

**Model name**: User, class: User -&gt; Capitalized U and singular

**File name**: user.rb -&gt; singular and all lowercase

**Controller file name**: users\_controller.rb, class: UsersController -&gt; camel case class name, snake case file name both plural

**Views folder**: users

**Table name**: users -&gt; plural of model

## Table Command

#### To generate a migration to create a table \(in this example articles\):

`rails generate migration create_articles`

#### To add attributes for the table in the migration file, add the following inside create\_table block:

`t.string :title`

`t.text :description`

`t.timestamps`

#### To run the migration file and create the articles table:

`rake db:migrate`

OR

`bundle exec rake db:migrate`

If using Rails 5 -&gt; `rails db:migrate`

#### To rollback a migration \(undo the last migration\):

`rake db:rollback`

If using Rails 5 -&gt; `rails db:rollback`

#### To add a column \(example: created\_at column\) to the articles table:

`rails generate migration add_created_at_to_articles`

Then within the def change method in the migration file:

`add_column :articles, :created_at, :datetime`

#### To add a different column \(example: name\) to a users table:

`rails generate migration add_name_to_users`

Then within the def change method in the migration file:

`add_column :users, :name, :string`

In the above two adding column methods, the first argument is the name of the table, second is the attribute name and third is the type

#### To create a model file for Article:

- In the app/models folder create a file called article.rb

- Fill it in with the following -&gt;

`class Article < ActiveRecord::Base`

`end`

If using Rails 5 -&gt;

`class Article < ApplicationRecord`

`end`

#### To start the rails console:

`rails console`

#### To test connection to the articles table:

`Article.all` \# classname.all will list all the articles in the articles table

Then simply type in `Article` \(classname\) to view the attributes

#### To create a new article with attributes title and description:

```ruby
article = Article.new(title: "This is a test title", description: "This is a test description")
article.save
```

OR

```ruby
article = Article.new
article.title = "This is a test title"
article.description = "This is a test description"
article.save
```

Another method to do the same:

`article = Article.create(title: "This is a test title", description: "This is a test description") # This will hit the table right away without needing the article.save line`

