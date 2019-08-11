# Complete Homepage

#### After completion of the prior video, below is what the application.html.erb looks like:

```markup
<!DOCTYPE html>
<html>
  <head>
    <title>AlphaBlog</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>
  
  <body>
    <%= render 'layouts/navigation' %>
    <%= render 'layouts/messages' %>
    <div class="container">
      <%= yield %>
    </div>
    <%= render 'layouts/footer' %>
  </body>
</html>
```

#### The image to be added as background for the jumbotron should be added in the app/assets/images folder

#### Below is what the custom.css.scss file looks like:

```css
$navbar-default-bg: #08088A;

// "bootstrap-sprockets" must be imported before "bootstrap" and "bootstrap/variables"
@import "bootstrap-sprockets";
@import "bootstrap";

#logo {
  float: left;
  font-size: 1.7em;
  color: #fff;
  text-transform: uppercase;
  letter-spacing: -1px;
  font-weight: bold;
}

#logo:hover {
  color: #fff;
  text-decoration: none;
}

.center {
  text-align: center;
}

.jumbotron {
  background-image: asset-url('background.png');
  background-size: cover;
  height: 550px;
}

.jumbotron h1 {
  color: #fff;
  text-align: center;
  margin-bottom: 30px;
  letter-spacing: -1px;
  font-weight: bold;
}

.btn-xlarge {
  font-size: 1.7em;
}

footer {
  margin-top: 45px;
  padding-top: 5px;
  border-top: 1px solid #eaeaea;
  color: #777;
}

footer a:hover {
  color: #222;
}

footer small {
  float: left;
}

footer ul {
  float: right;
  list-style: none;
}

footer ul li {
  float: left;
  margin-left: 15px;
}
```

#### Below is what the \_navigation.html.erb file looks like:

```markup
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <%= link_to "Alpha Blog", root_path, class: "navbar-brand", id: "logo" %>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li><%= link_to "Articles", articles_path %></li>
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Actions <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><%= link_to "New Article", new_article_path %> </li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">One more separated link</a></li>
          </ul>
        </li>
      </ul>
      <form class="navbar-form navbar-left">
        <div class="form-group">
          <input type="text" class="form-control" placeholder="Search">
        </div>
        <button type="submit" class="btn btn-default">Submit</button>
      </form>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#">Link</a></li>
        <li class="dropdown">
          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#">Action</a></li>
            <li><a href="#">Another action</a></li>
            <li><a href="#">Something else here</a></li>
            <li role="separator" class="divider"></li>
            <li><a href="#">Separated link</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
```

#### Below is what the \_footer.html.erb file looks like:

```markup
<div class="container">
  <footer class="footer">
    <small>
      Copyright &copy; <a href="https://github.com/lu1995happy/Alpha-blog">Alpha Blog Project</a>
      by <strong>Tianlin Lu</strong>
    </small>
    <nav>
      <ul>
        <li><%= link_to "About", about_path %></li>
      </ul>
    </nav>
  </footer>
</div>
```

