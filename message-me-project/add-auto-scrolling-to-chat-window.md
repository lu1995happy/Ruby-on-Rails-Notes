# Add auto-scrolling to chat window

## `views/chatroom/index.html.erb`

```markup
<div class="content" id="messages">
  <div class="ui feed" id="message-container">
    <%= render @messages %>
  </div>
</div>
```

## `custom.css.scss`

```css
#messages {
  height: 15em;
  overflow: auto;
}
```

## `application.js`

```javascript
scroll_bottom = function() {
  if ($('#messages').length > 0) {
    $('#messages').scrollTop($('#messages')[0].scrollHeight);
  }
}

$(document).on('turbolinks:load', function () {
  $('.ui.dropdown').dropdown();
  $('.message .close').on('click', function () {
    $(this).closest('.message').transition('fade');
  });
  scroll_bottom();
})
```

## `channels/chatroom.coffee`

```coffeescript
received: (data) ->
  # Called when there's incoming data on the websocket for this channel
  $('#message-container').append data.mod_message
  scroll_bottom()
```

