# Complete Homepage

After completion of the prior video, below is what the application.html.erb looks like:

&lt;!DOCTYPE html&gt;

&lt;html&gt;

&lt;head&gt;

&lt;title&gt;AlphaBlog&lt;/title&gt;

&lt;%= stylesheet\_link\_tag 'application', media: 'all', 'data-turbolinks-track' =&gt; true %&gt;

&lt;%= javascript\_include\_tag 'application', 'data-turbolinks-track' =&gt; true %&gt;

&lt;%= csrf\_meta\_tags %&gt;

&lt;/head&gt;

&lt;body&gt;

&lt;%= render 'layouts/navigation' %&gt;

&lt;%= render 'layouts/messages' %&gt;

&lt;div class="container"&gt;

&lt;%= yield %&gt;

&lt;/div&gt;

&lt;%= render 'layouts/footer' %&gt;

&lt;/body&gt;

&lt;/html&gt;

The image to be added as background for the jumbotron should be added in the app/assets/images folder

Below is what the custom.css.scss file looks like:

$navbar-default-bg: black;

@import "bootstrap-sprockets";

@import "bootstrap";

\#logo {

float: left;

font-size: 1.7em;

color: \#fff;

text-transform: uppercase;

letter-spacing: -1px;

font-weight: bold;

}

\#logo:hover {

color: \#fff;

text-decoration: none;

}

.center {

text-align: center;

}

.jumbotron {

background-image: asset-url\('new\_cover\_page.png'\);

background-size: cover;

height: 550px;

}

.jumbotron h1 {

color: \#fff;

text-align: center;

margin-bottom: 30px;

letter-spacing: -1px;

font-weight: bold;

}

.btn-xlarge {

font-size: 1.7em;

background-color: black;

}

footer {

margin-top: 45px;

padding-top: 5px;

border-top: 1px solid \#eaeaea;

color: \#777;

}

footer a:hover {

color: \#222;

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

Below is what the \_navigation.html.erb file looks like:

&lt;nav class="navbar navbar-default"&gt;

&lt;div class="container-fluid"&gt;

&lt;!-- Brand and toggle get grouped for better mobile display --&gt;

&lt;div class="navbar-header"&gt;

&lt;button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="\#bs-example-navbar-collapse-1" aria-expanded="false"&gt;

&lt;span class="sr-only"&gt;Toggle navigation&lt;/span&gt;

&lt;span class="icon-bar"&gt;&lt;/span&gt;

&lt;span class="icon-bar"&gt;&lt;/span&gt;

&lt;span class="icon-bar"&gt;&lt;/span&gt;

&lt;/button&gt;

&lt;%= link\_to "Alpha blog", root\_path, class: "navbar-brand", id: "logo" %&gt;

&lt;/div&gt;

&lt;!-- Collect the nav links, forms, and other content for toggling --&gt;

&lt;div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1"&gt;

&lt;ul class="nav navbar-nav"&gt;

&lt;li&gt;&lt;%= link\_to "Articles", articles\_path %&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Link&lt;/a&gt;&lt;/li&gt;

&lt;li class="dropdown"&gt;

&lt;a href="\#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false"&gt;Actions &lt;span class="caret"&gt;&lt;/span&gt;&lt;/a&gt;

&lt;ul class="dropdown-menu"&gt;

&lt;li&gt;&lt;%= link\_to "New Article", new\_article\_path %&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Another action&lt;/a&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Something else here&lt;/a&gt;&lt;/li&gt;

&lt;li role="separator" class="divider"&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Separated link&lt;/a&gt;&lt;/li&gt;

&lt;li role="separator" class="divider"&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;One more separated link&lt;/a&gt;&lt;/li&gt;

&lt;/ul&gt;

&lt;/li&gt;

&lt;/ul&gt;

&lt;form class="navbar-form navbar-left" role="search"&gt;

&lt;div class="form-group"&gt;

&lt;input type="text" class="form-control" placeholder="Search"&gt;

&lt;/div&gt;

&lt;button type="submit" class="btn btn-default"&gt;Submit&lt;/button&gt;

&lt;/form&gt;

&lt;ul class="nav navbar-nav navbar-right"&gt;

&lt;li&gt;&lt;a href="\#"&gt;Link&lt;/a&gt;&lt;/li&gt;

&lt;li class="dropdown"&gt;

&lt;a href="\#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false"&gt;Dropdown &lt;span class="caret"&gt;&lt;/span&gt;&lt;/a&gt;

&lt;ul class="dropdown-menu"&gt;

&lt;li&gt;&lt;a href="\#"&gt;Action&lt;/a&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Another action&lt;/a&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Something else here&lt;/a&gt;&lt;/li&gt;

&lt;li role="separator" class="divider"&gt;&lt;/li&gt;

&lt;li&gt;&lt;a href="\#"&gt;Separated link&lt;/a&gt;&lt;/li&gt;

&lt;/ul&gt;

&lt;/li&gt;

&lt;/ul&gt;

&lt;/div&gt;&lt;!-- /.navbar-collapse --&gt;

&lt;/div&gt;&lt;!-- /.container-fluid --&gt;

&lt;/nav&gt;

Below is what the \_footer.html.erb file looks like:

&lt;div class="container"&gt;

&lt;footer class="footer"&gt;

&lt;small&gt;

Copyright © &lt;a href="enter in a link here"&gt;The Complete Ruby on Rails Developer&lt;/a&gt;

by &lt;a href="enter in a link here"&gt;Mashrur Hossain&lt;/a&gt;

&lt;/small&gt;

&lt;nav&gt;

&lt;ul&gt;

&lt;li&gt;&lt;%= link\_to "About", about\_path %&gt;&lt;/li&gt;

&lt;/ul&gt;

&lt;/nav&gt;

&lt;/footer&gt;

&lt;/div&gt;

