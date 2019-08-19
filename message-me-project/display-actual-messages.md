# Display actual messages

## `views/chatroom/index.html.erb`

```markup
<div class="ui two column grid">
  <div class="twelve wide column">
    <div class="ui fluid raised card chatbox">
      <div class="content">
        <div class="ui feed">
          <% @messages.each do |message| %>
            <div class="event">
              <div class="content">
                <div class="summary">
                  <em><%= message.user.username %></em>: <%= message.body %>
                </div>
              </div>
            </div>
          <% end %>
        </div>
      </div>
      <div class="extra content">
        <form class="ui reply form">
          <div class="field">
            <div class="ui fluid icon input">
              <input type="text" placeholder="Enter a message...">
              <i class="bordered inverted orange edit icon"></i>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
```

## `chatroom_controller.rb`

```ruby
class ChatroomController < ApplicationController

   def index
      @messages = Message.all
   end

end
```

