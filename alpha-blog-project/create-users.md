# Create Users

#### To create a feature branch:

`git checkout -b nameofbranch`

#### To create a feature branch named create-users:

`git checkout -b create-users`

#### To view list of branches:

`git branch`

#### To move to master branch:

`git checkout master`

#### To move to already created feature branch:

`git checkout nameofbranch`

#### Important to remember is to always have master branch deployable to production and work on all new features and additions in feature branches

#### To create a migration to create users table:

`rails generate migration create_users`

#### Then within the migration file add in the following within the create\_table block to add the username, email and timestamps columns \(created\_at and updated\_at\):

`t.string :username`

`t.string :email`

`t.timestamps`

#### To run the migration file and create the users table:

`rake db:migrate`

#### Add a user.rb model file under app/models folder and fill in the following:

```ruby
class User < ActiveRecord::Base
end
```

#### Then start rails console and test out connections:

`rails console`

`User.all`

`User`

`user = User.create(username: "test", email: "test@example.com")`

`user = User.create(username: "test2", email: "test2@example.com")`

#### To grab first user and update their email address:

`user = User.find(1)`

#### OR

`user = User.first`

`user.email = "test3@example.com"`

`user.save`

#### To destroy user with id = 2:

`user = User.find(2)`

`user.destroy`

#### To make a commit of the changes made in the feature branch:

`git add -A`

`git commit -m "create users table and user model"`

#### To merge the changes in the feature branch to the master branch first switch to master branch:

`git checkout master`

`git merge nameofbranch`

`git push to push code to repository`

#### To delete a feature branch that is no longer needed and has been merged to master already:

`git branch -d nameofbranch`

#### To delete a feature branch that is no longer needed but has NOT been merged to master:

`git branch -D nameofbranch`

