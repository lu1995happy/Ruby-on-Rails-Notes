# Display messages realtime

## `javascripts/channels/chatroom.coffee`

```coffeescript
received: (data) ->
  # Called when there's incoming data on the websocket for this channel
  $('#message-container').append data.mod_message
```

## `messages_controller.rb`

```ruby
def create
  message = current_user.messages.build(message_params)
  if message.save
    ActionCable.server.broadcast "chatroom_channel",
                                  mod_message: message_render(message)
  end
end
```

## `views/chatroom/index.html.erb`

```markup
<div class="ui fluid raised card chatbox">
  <div class="content">
    <div class="ui feed" id="message-container">
      <%= render @messages %>
    </div>
  </div>
  <div class="extra content">
    <%= form_for(@message, html: {class: "ui reply form", role: "form"}, url: message_path, remote: true) do |f| %>
      <div class="field">
        <div class="ui fluid icon input">
          <%= f.text_field :body %>
          <%= f.button '<i class="bordered inverted orange edit icon"></i>'.html_safe %>
        </div>
      </div>
    <% end %>
  </div>
</div>
```

