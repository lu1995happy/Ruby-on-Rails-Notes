# Add dropdown, nav partial and favicon

## `application.html.erb`

```markup
<!DOCTYPE html>
<html>
  <head>
    <title>MessageMe</title>
    <%= favicon_link_tag %>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <div class="ui small inverted menu">
      <div class="ui container">
        <%= render 'layouts/navigation'%>
      </div>
    </div>
    <div class="ui container">
      <%= yield %>
    </div>
  </body>
</html>
```

## `application.js`

```javascript
$(document).on('turbolinks:load', function () {
  $('.ui.dropdown').dropdown();
})
```

## `_navigation.html.erb`

```markup
<a class="item">
  Chatroom
</a>
<a class="item">
  Messages
</a>
<div class="right menu">
  <div class="ui dropdown item">
    Account <i class="dropdown icon"></i>
    <div class="menu">
      <a class="item">Log out</a>
      <a class="item">Log in</a>
      <a class="item">Sign up</a>
    </div>
  </div>
  <div class="item">
      <div class="ui primary button">Sign Up</div>
  </div>
</div>
```

