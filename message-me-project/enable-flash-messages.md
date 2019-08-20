# Enable flash messages

## `javascripts/application.js`

```javascript
$(document).on('turbolinks:load', function () {
  $('.ui.dropdown').dropdown();
  $('.message .close').on('click', function () {
    $(this).closest('.message').transition('fade');
  });
})
```

## `_message.html.erb`

```markup
<% flash.each do |message_type, message_content| %>
  <div class="ui <%= message_type %> message transition">
    <i class="close icon"></i>
    <div class="header">
      <%= message_content %>
    </div>
  </div>
<% end %>
```

## `application.html.erb`

```markup
<div class="ui container">
    <%= render 'layouts/messages' %>
    <%= yield %>
</div>
```

