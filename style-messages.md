# Style Messages

#### In your articles\_controller.rb file change the flash\[:notice\] to be flash\[:success\], there should be 3 such occurances in that file

#### Update your \_messages.html.erb file with the following code:

```markup
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <% flash.each do |name, msg| %>
      <div class='alert alert-<%="#{name}" %>'>
        <a href="#" class="close" data-dismiss="alert">×</a>
        <%= content_tag :div, msg, :id => "flash_#{name}" if msg.is_a?(String) %>
      </div>
    <% end %>
  </div>
</div>
```

#### Update your \_form.html.erb at the top to remove the error portion and replace it with the following:

`<%= render 'shared/errors', obj: @article %>`

#### Create a folder called shared under app/views/ folder. Then within the shared folder file named \_errors.html.erb to create the errors partial, then fill it in with the following code:

```markup
<% if obj.errors.any? %>
  <div class="row">
    <div class="col-xs-8 col-xs-offset-2">
      <div class="panel panel-danger">
        <div class="panel-heading">
          <h2 class="panel-title">
            <%= pluralize(obj.errors.count, "error") %>
            prohibited this article from being saved:
          </h2>
          <div class="panel-body">
            <ul>
              <% obj.errors.full_messages.each do |msg| %>
                <li><%= msg %></li>
              <% end %>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
<% end %>
```

