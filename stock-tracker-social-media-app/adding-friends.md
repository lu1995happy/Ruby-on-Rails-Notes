# Adding Friends

#### Add the friendship route in `config/routes.rb` file:

`get 'my_friends', to: 'users#my_friends'`

#### In the `users_controller.rb` file and add in this action:

```ruby
def my_friends

end
```

#### Add in the view, under app/views/users folder create a `my_friends.html.erb` file:

`<h1>My Friends</h1>`

#### Now add the friendship model, generate it:

`rails generate model Friendship`

#### Add the associations-&gt; in `friendship.rb` model file:

`belongs_to :user` 

`belongs_to :friend, :class_name => 'User'`

#### in the `user.rb` model file:

`has_many :friendships` 

`has_many :friends, through: :friendships`

#### Add in the updates to the latest migration file that got created:

```ruby
def change
  create_table :friendships do |t|
    t.belongs_to :user
    t.belongs_to :friend, class: 'User'
    t.timestamps
  end
end
```

#### Run the migration file, rake db:migrate \(or `rails db:migrate` for rails 5\)

