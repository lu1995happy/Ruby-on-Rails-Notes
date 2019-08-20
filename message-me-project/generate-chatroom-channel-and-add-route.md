# Generate chatroom channel and add route

## Command

### create chatroom channel

`rails generate channel chatroom`

## `channels/chatroom_channel.rb`

```ruby
class ChatroomChannel < ApplicationCable::Channel
  def subscribed
    stream_from "chatroom_channel"
  end

   def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end
```

## `routes.rb`

```ruby
Rails.application.routes.draw do
  root 'chatroom#index'
  get 'login', to: 'sessions#new'
  post 'login', to: 'sessions#create'
  delete 'logout', to: 'sessions#destroy'
  post 'message', to: 'messages#create'

  mount ActionCable.server, at: '/cable'
end
```

