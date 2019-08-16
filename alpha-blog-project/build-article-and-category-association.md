# Build Article and Category Association

### To generate a migration file to create the article\_categories table

`rails generate migration create_article_categories`

### Within the migration file add in the following to add article\_id and category\_id to the table

`t.integer :article_id`

`t.integer :category_id`

### Run `rake db:migrate` to create the table

`rake db:migrate`

### Create a model file named `article_category.rb` under the `app/models` folder and fill it in

```ruby
class ArticleCategory < ApplicationRecord
  # Note Rails 4 -> class ArticleCategory < ActiveRecord::Base
  belongs_to :article
  belongs_to :category
end
```

### Update the `article.rb` and `category.rb` model files to include the following lines

```ruby
# article.rb ->
has_many :article_categories
has_many :categories, through: :article_categories

# category.rb -> 
has_many :article_categories
has_many :articles, through: :article_categories
```

### Then hop on the rails console and test out the associations

```ruby
ArticleCategory.all
ArticleCategory
article = Article.last
category = Category.last
article.categories
article.categories << category
category.articles
category.articles << article
```

