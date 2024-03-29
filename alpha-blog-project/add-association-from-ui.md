# Add Association from UI

## Update the `_form.html.erb` partial under the `app/views/articles` folder and add the part to associate categories

```markup
<%= render 'shared/errors', obj: @article %>

<div class='row'>
  <div class='col-xs-12'>
    <%= form_for(@article, :html => {class: "form-horizontal", role: "form"}) do |f| %>
      <div class="form-group">
        <div class="control-label col-sm-2">
          <%= f.label :title %>
        </div>
        <div class="col-sm-8">
          <%= f.text_field :title, class: "form-control", placeholder: "Title of article", autofocus: true %>
        </div>
      </div>
      <div class="form-group">
        <div class="control-label col-sm-2">
          <%= f.label :description %>
        </div>
        <div class="col-sm-8">
          <%= f.text_area :description, rows: 10, class: "form-control", placeholder: "Body of article" %>
        </div>
      </div>
      <div class="form-group">
        <div class="row">
          <div class="col-sm-offset-2 col-sm-8">
            <%= f.collection_check_boxes :category_ids, Category.all, :id, :name do |cb| %>
              <% cb.label(class: "checkbox-inline input_checkbox") {cb.check_box(class: "checkbox") + cb.text} %>
            <% end %>
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="col-sm-offset-2 col-sm-10">
          <%= f.submit class: 'btn btn-primary btn-lg' %>
        </div>
      </div>
    <% end %>
    <div class="col-xs-4 col-xs-offset-4">
      [ <%= link_to "Cancel request and return to articles listing", articles_path %> ]
    </div>
  </div>
</div>
```

## Update the article\_params method under private in the `articles_controller.rb` file to allow category\_ids

```ruby
def article_params
    params.require(:article).permit(:title, :description, category_ids: [])
end
```

