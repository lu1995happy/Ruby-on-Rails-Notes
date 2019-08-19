# Add message partial

## `views/messages/_message.html.erb`

```markup
<div class="event">
  <div class="content">
    <div class="summary">
      <em><%= message.user.username %></em>: <%= message.body %>
    </div>
  </div>
</div>
```

## `views/chatroom/index.html.erb`

```markup
<div class="content">
  <div class="ui feed">
    <%= render @messages %>
  </div>
</div>
```

