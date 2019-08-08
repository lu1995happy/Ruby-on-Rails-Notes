# Edit, Delete and Validations

## Table Command

#### To find an article with id 2 and edit it's title:

```ruby
article = Article.find(2) # Here assumption is article with id of 2 was being looked for
article.title = "This is an edited title"
article.save
```

#### To delete an article, example with id 5:

```ruby
article = Article.find(5)
article.destroy
```

#### To add validations presence and length validations to article model for title and description:

```ruby
class Article < ActiveRecord::Base
    validates :title, presence: true, length: {minimum: 3, maximum: 50}
    validates :description, presence: true, length: {minimum: 10, maximum: 300}
end
```

If using Rails 5, the first line above would be -&gt; `class Article < ApplicationRecord`

#### To find errors in article object while saving \(if it's rolled back\):

```ruby
article.errors.any?
article.errors.full_messages
```

