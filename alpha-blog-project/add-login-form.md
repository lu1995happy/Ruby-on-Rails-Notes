# Add Login Form

#### Add the login/logout routes in the config/routes.rb file:

`get 'login', to: 'sessions#new'`

`post 'login', to: 'sessions#create'`

`delete 'logout', to: 'sessions#destroy'`

#### Create a sessions\_controller.rb file under app/controllers folder and fill it in with the following:

```ruby
class SessionsController < ApplicationController
    def new
    end
    def create
    end
    def destroy
    end
end
```

#### Create a new folder under app/views called sessions, then within the sessions folder create a new file called new.html.erb and fill it in with the following, this will be your log in form:



