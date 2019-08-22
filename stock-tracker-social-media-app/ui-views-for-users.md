# UI Views for Users

#### Now add some styling for the classes introduced in `application.css.scss`:

```css
.left-padding {
  padding-left: 15px !important;
}

.logout {
  padding-left: 0;
}

.user-name {
  padding-top: 15px;
}

.nav.navbar-right li {
  .btn {
    color: #fff !important;
    margin-top: 5%;
  }
  .btn-danger:hover {
    background-color: darken(#d9534f, 20%) !important;
  }
}
```

#### Now move the navigation code to a `_navigation.html.erb` partial under app/views/layouts folder

```markup
<div class="navbar navbar-default navbar-static-top">
  <div class="container">
    <%= link_to "Finance Tracker", root_path, class: "navbar-brand" %>
    <% if current_user %>
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-responsive-collapse">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>

      <div class="navbar-collapse collapse navbar-responsive-collapse">
        <ul class="nav navbar-nav col-md-6">
          <li><%= link_to "My Portfolio", my_portfolio_path  %></li>
          <li><%= link_to "My Profile", edit_registration_path(current_user) %></li>
          <li><%= link_to "link3", "#" %></li>
        </ul>
        <ul class="nav navbar-right col-md-4">
          <li class="col-md-8 user-name text-right">
            <i class="fa fa-user"></i>
            <%= current_user.full_name.present? ? current_user.full_name : current_user.email %>
          </li>
          <li class="col-md-4 logout">
            <%= link_to("logout", destroy_user_session_path,
                                class: "btn btn-xs btn-danger", method: :delete) %>
          </li>
        </ul>
      </div>
    <% end %>
  </div>
</div>
```

#### Then in the `application.html.erb` reference this by adding the code below:

`<%= render 'layouts/navigation' %>`

