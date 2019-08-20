# Add method to broadcast messages

## `javascripts/channels/chatroom.coffee`

```coffeescript
received: (data) ->
  # Called when there's incoming data on the websocket for this channel
  alert data.foo
```

## `messages_controller.rb`

```ruby
def create
  message = current_user.messages.build(message_params)
  if message.save
    ActionCable.server.broadcast "chatroom_channel",
                                  foo: message.body
  end
end
```

## `config/environments/development.rb`

```ruby
# config.action_cable.disable_request_forgery_protection = true
# config.action_cable.allowed_request_origins = ['https://mashrur-messageme_test.herokuapp.com']
```

