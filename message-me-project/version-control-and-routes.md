# Version Control and Routes

## Version Control

#### When creating github repo for application ensure you click the SSH button then push existing repo:

`git remote add origin git@github.com:yourgithubaccountname/alpha-blog.git`

`git push -u origin master` \# Remember you only need to use this command the first time

#### To view remotes setup in your environment \(from your app directory\):

`git remote -v`

#### For future pushes to repository:

`git push`

## Add Root and Login Routes

### Controllers

```ruby
# chatroom_controller.rb
class ChatroomController < ApplicationController
   def index
   end
 end
 
 # sessions_controller.rb
 class SessionsController < ApplicationController
   def new
   end
 end
```

### Views

```markup
# chatroom/index.html.erb
<h1>You have reached the root route</h1>

# sessions/new.html.erb
<h1>You have reached the login page</h1>
```

### Routes

```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
  root 'chatroom#index'
  get 'login', to: 'sessions#new'
end
```

