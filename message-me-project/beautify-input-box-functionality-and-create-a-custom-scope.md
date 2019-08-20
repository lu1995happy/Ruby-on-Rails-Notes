# Beautify input box, functionality and create a custom scope

## `application.js`

```javascript
scroll_bottom = function() {
  if ($('#messages').length > 0) {
    $('#messages').scrollTop($('#messages')[0].scrollHeight);
  }
}

submit_message = function() {
  $('#message_body').on('keydown', function(e) {
    if (e.keyCode == 13) {
      $('button').click();
      e.target.value = "";
    };
  });
};

$(document).on('turbolinks:load', function () {
  $('.ui.dropdown').dropdown();
  $('.message .close').on('click', function () {
    $(this).closest('.message').transition('fade');
  });
  scroll_bottom();
  submit_message();
})
```

## `custom.css.scss`

```css
@import "semantic-ui";

.chatbox {
  height: 450px;
}

#messages {
  height: 15em;
  overflow: auto;
}

.input {
  button {
    display:none;
  }
}
```

## `models/message.rb`

```ruby
class Message < ApplicationRecord
  belongs_to :user
  validates :body, presence: true
  scope :custom_display, -> { order(:created_at).last(20) }
end
```

## `chatroom_controller.rb`

```ruby
def index
	@message = Message.new
    @messages = Message.custom_display
end
```

