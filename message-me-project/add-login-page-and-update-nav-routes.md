# Add login page and update nav routes

## `views/sessions/new.html.erb`

```markup
<h2 class="ui center aligned large header">
  Welcome to MessageMe - <em>a complete Chat App</em>
</h2>

 <h4 class="ui center aligned medium icon header">
  <i class="circular orange power off tiny icon"></i>
  Log in to continue
</h4>

 <div class="ui placeholder segment">
  <div class="ui two column very relaxed stackable grid">
    <div class="column">
      <form class="ui form">
        <div class="field">
          <label>Username</label>
          <div class="ui left icon input">
            <input type="text" placeholder="Username">
            <i class="user icon"></i>
          </div>
        </div>
        <div class="field">
          <label>Password</label>
          <div class="ui left icon input">
            <input type="text" placeholder="Password">
            <i class="lock icon"></i>
          </div>
        </div>
        <button class="ui orange submit button">Login</button>
      </form>
    </div>
    <div class="middle aligned column">
      <div class="ui big orange disabled button">
        <i class="signup icon"></i>
        Sign Up
      </div>
    </div>
  </div>
  <div class="ui vertical divider">
    Or
  </div>
</div> 
```

## `_navigation.html.erb`

```markup
<%= link_to "Chatroom", root_path, class: "item" %>
<a class="item">
  Messages
</a>
<div class="right menu">
  <div class="ui dropdown item">
    Account <i class="dropdown icon"></i>
    <div class="menu">
      <a class="item">Log out</a>
      <%= link_to "Log in", login_path, class: "item" %>
      <a class="item">Sign up</a>
    </div>
  </div>
  <div class="item">
      <div class="ui primary button">Sign Up</div>
  </div>
</div>
```

