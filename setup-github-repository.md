# Setup Github Repository

## Git

#### To display your public SSH key:

`cat ~/.ssh/id_rsa.pub`

#### When creating github repo for application ensure you click the SSH button then push existing repo:

`git remote add origin git@github.com:yourgithubaccountname/alpha-blog.git`

`git push -u origin master` \# Remember you only need to use this command the first time

#### To view remotes setup in your environment \(from your app directory\):

`git remote -v`

#### For future pushes to repository:

`git push`

