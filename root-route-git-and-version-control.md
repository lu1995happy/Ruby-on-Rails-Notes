# Root Route, Git and Version Control

## Routes

#### To set root route to pages controller home:

Navigate to config/routes.rb file and enter in the following code -&gt;

`root 'pages#home'`

## Git

The reference to the root path within the application code would be root\_path

#### First time \(required only once to configure git for your environment\):

`git config --global user.name "Your name"`

`git config --global user.email "Your email"`

replace Your name and Your email above with your actual name and email address which you want shown on repo

#### To display git config settings:

`git config --list`

Some useful git commands:

#### To initialize a git repository for your application \(do this from within the application directory\) -&gt;

`git init`

Note: if using Rails 5, your application will already come with a git repository initiated, if you initiate a new one, it'll simply do the same step again

#### To add/track all files -&gt;

`git add -A`

#### To commit changes/updates/additions to repository -&gt;

`git commit -m "A useful message to help remember details of commit"`

#### To check current state of file updates with already committed code in repo -&gt;

`git status`

#### To reject latest changes -&gt;

`git checkout -f`

