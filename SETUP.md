# Setup - Docker

$ = Non Root User

&#35; = Root User


git clone https://username@github.com/username/repository.git

git remote set-url origin https://username@github.com/username/repository_name.git


## Create Git Repository
1. Crate Git Repository on github.com. This will be empty repository with "main" as default branch.


## Changing the default branch
1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click  Settings.
3. Under your repository name, click  Settings.
4. Under "Default branch", to the right of the default branch name, click .
5. Rename "main" to "master".


## Clone Git Repository
1. Clone Git Repository in project folder
```
$ git clone git@github.com:username/repository_name.git .
```

2. First commit in repository. Copy sample file into repository folder(Eg. SETUP.md)
```
$ git add SETUP.md
$ git commit -m "first commit"
$ git push -u origin master
```

--------------------------------------------------------------------------------
## Generating a new SSH key
1. Generate a new SSH key on your local machine
```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```
--------------------------------------------------------------------------------

3. Create development (develop) branch
```
$ git checkout -b develop origin/master
```


## Add the Framework Repository to project repository
1. Add the framework's repository
```
$ git remote add laravel git@github.com:laravel/laravel.git
```
2. Check project repositories
```
$ git remote -v
```

3. Gather information from the framework repository master branch
```
$ git fetch laravel master
```

4. Create a separate branch named framework that matches and pulls in the most recent version of Laravel.
```
$ git checkout -b framework laravel/master
```

5. Go back to develop branch and merge framework branch
```
$ git checkout develop
$ git merge framework --allow-unrelated-histories
```

6. Push develop branch to remote repository
```
$ git push origin develop
```

--------------------------------------------------------------------------------
