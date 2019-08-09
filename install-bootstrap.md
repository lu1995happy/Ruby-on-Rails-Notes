# Install Bootstrap

#### Bootstrap sass gem page:

[https://github.com/twbs/bootstrap-sass](https://github.com/twbs/bootstrap-sass)

#### Add the following gem to your gemfile above the gem 'sass-rails':

`gem 'bootstrap-sass', '~> 3.3.5'`

#### To install the gem to your app run:

`bundle install --without production`

#### Create a file called custom.css.scss under app/assets/stylesheets folder

#### Add the following lines to the file:

`@import "bootstrap-sprockets";`

`@import "bootstrap";`

#### Add the following line to your application.js file in the app/assets/javascripts folder under the line that says //= require jquery\_ujs:

`//= require bootstrap-sprockets`

