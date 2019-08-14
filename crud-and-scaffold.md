# CRUD and Scaffold

## Query language to communicate with database: SQL \(Structured Query Language\)

#### CRUD actions:

* C - Create
* R - Read
* U - Update
* D - Delete

## Scaffold generator command to create Article model, articles controller, views for articles and migration file to create articles table:

`rails generate migration create_users`

`rails generate scaffold Article title:string description:text`

`rails generate scaffold Comment description:text user:references`

`rails destroy scaffold Comment`

`rails console`

#### Command to see routes present for your app:

`rake routes`

If using Rails 5, `rails routes`

#### The line resources :articles in the config/routes.rb file provides the following routes:

* index of articles \(listing\)
* new article
* create article
* edit article
* update article \(put and patch\)
* show article
* delete article

#### From UI perspective -&gt;

index lists all the articles in the db of the app

* new article deals with the form to enter in new article details
* create handles the submission of the items in the new article form
* edit article deals with the form to enter in edit details for an existing article
* update article deals with the submission of the edited details
* show article displays an individual article based on selection
* delete article deletes an article from the db

