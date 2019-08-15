# Sign in Upon Signup

## Update the users controller create action to look like the following

```ruby
def create
  @user = User.new(user_params)
  if @user.save
    session[:user_id] = @user.id
    flash[:success] = "Welcome to the alpha blog #{@user.username}"
    redirect_to user_path(@user)
  else
    render 'new'
  end
end
```

