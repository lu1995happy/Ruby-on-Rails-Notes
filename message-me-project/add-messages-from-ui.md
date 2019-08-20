# Add messages from UI

## Command

### create the messages controller

`rails generate controller messages create`

### destroy all the messages controller related files

`rails destroy controller messages`

## `chatroom_controller.rb`

```ruby
class ChatroomController < ApplicationController

  before_action :require_user

	def index
		@message = Message.new
    @messages = Message.all
  end

end
```

## `messages_controller.rb`

```ruby
class MessagesController < ApplicationController
  before_action :require_user

  def create
    message = current_user.messages.build(message_params)
    if message.save
      redirect_to root_path
    end
  end

  private

    def message_params
      params.require(:message).permit(:body)
    end

 end
```

## `chatroom/index.html.erb`

```markup
<div class="extra content">
  <%= form_for(@message, html: {class: "ui reply form", role: "form"}, url: message_path) do |f| %>
    <div class="field">
      <div class="ui fluid icon input">
        <%= f.text_field :body %>
        <%= f.button '<i class="bordered inverted orange edit icon"></i>'.html_safe %>
      </div>
    </div>
  <% end %>
</div>
```

## `routes.rb`

```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
  root 'chatroom#index'
  get 'login', to: 'sessions#new'
  post 'login', to: 'sessions#create'
  delete 'logout', to: 'sessions#destroy'
  post 'message', to: 'messages#create'
end
```

