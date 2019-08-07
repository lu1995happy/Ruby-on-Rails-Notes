# Production Deploy

## Prepartion for heroku deploy

* Remove sqlite3 gem from top of application to within group :development, :test do block
* Create a group production -&gt;

```ruby
group :production do
    gem 'pg', '~> 0.11'
    gem 'rails_12factor'
end
```

If using Rails 5, then

```ruby
group :production do
    gem 'pg', '~> 0.11'
end
```

* Save Gemfile
* Run `bundle install` --without production to update Gemfile.lock file
*  Commit your changes to git repo -&gt;
  * `git add -A`
  * `git commit -m "Make app production ready"`

## Command to install heroku toolbelt to your local environment

`wget -qO-` [`https://toolbelt.heroku.com/install-ubuntu.sh`](https://toolbelt.heroku.com/install-ubuntu.sh) `| sh`

#### Check heroku:

`heroku -v`

`heroku version`

`heroku` \# for list of common heroku commands

#### To login to your heroku account from your env -&gt;

`heroku login`

#### To add your SSH key to your heroku account so you don't have to use username and password everytime -&gt;

`heroku keys:add`

#### To create a new production version of your app hosted in heroku -&gt;

`heroku create`

#### To push your application code to heroku \(deploy your app\) -&gt;

`git push heroku master`

#### **Ensure you have committed all your local changes to your git repo prior to pushing to heroku by checking git status**

#### To change the name of your application -&gt;

`heroku rename newnameofyourapp`

replace newnameofyourapp above with the name you'd like to give your app

Your app will then be accessible from the following browser URL -&gt;

newnameofyourapp.herokuapp.com

