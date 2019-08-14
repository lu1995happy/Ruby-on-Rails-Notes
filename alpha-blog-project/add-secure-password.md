# Add Secure Password

#### To create a migration to add password\_digest column to users table:

`rails generate migration add_password_digest_to_users`

#### Then pull up the migration file and fill in the column details within the def change block:

`add_column :users, :password_digest, :string`

#### Then save the file and run rake db:migrate to make the change to the table

#### In the model file \(user.rb\) add the following method:

`has_secure_password`

#### In the gemfile add the gem:

`gem 'bcrypt', '~> 3.1.7'`

#### Run the following from the command line:

`bundle install --without production`

#### Test it out from the rails console by creating a couple of test users and updating password for an existing user

#### To authenticate and test password for a user, first grab the user:

`user = User.last # (or User.find(enter id of user here))`

`user.authenticate("providecorrectpassword") # This will return the user object`

`user.authenticate("enterincorrectpassword") # This will return false`

