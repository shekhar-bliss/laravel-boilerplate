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
$ git fetch laravel 9.x

// In case of framework branch already exists
$ git pull laravel 9.x
```

4. Create a separate branch named framework that matches and pulls in the most recent version of Laravel.
```
$ git checkout -b framework laravel/9.x
```

5. Go back to develop branch and merge framework branch
```
$ git checkout develop
$ git merge framework --allow-unrelated-histories --squash
```

6. Push develop branch to remote repository
```
$ git push origin develop
```

--------------------------------------------------------------------------------

## Creating a release branch
Release branches are created from the develop branch.
1. Branch off and give the release branch a name reflecting the version number
```
$ git checkout -b release-0.1 origin/develop
```
2. Checkout to master branch
```
$ git checkout master
```

3. Merge release branch into master
```
$ git merge --no-ff release-0.1
```

4. that commit on master must be tagged for easy future reference to this historical version
```
$ git tag -a v0.1 -m "Laravel v9.3.4 Framework"
```

5. Push tag to remote repository
```
$ git push origin v0.1
```

6. Push master branch to remote repository
```
$ git push origin master
```

--------------------------------------------------------------------------------

## Docker : Installing Composer Dependencies
1. Directory Permissions
ug+rwx => 775
```
$ sudo chown -R $USER:www-data /path/to/your/laravel/root/directory
```

2. A small Docker container containing PHP and Composer to install the application's dependencies:
```
$ docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    composer install --ignore-platform-reqs
```

3. Copy .env.example file to .env and change db variable values accordingly in it
```
$ cp .env.docker .env
```

4. Installing Sail Into Clone Laravel application repository via docker
```
$ docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    php artisan sail:install
```

5. Change .env variable values accordingly
```
APP_PORT=82

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel_boilerplate
DB_USERNAME=sail
DB_PASSWORD=password
FORWARD_DB_PORT=3302

VITE_PORT=5172
```

6. Start Sail
```
$ ./vendor/bin/sail up
```

7. The first time you run the Sail up command, Sail's application containers will be built on your machine. This could take several minutes.
Once the application's Docker containers have been started, you can access the application in your web browser at: http://localhost:{APP_PORT}.

8. Running Migrations via sail
```
$ ./vendor/bin/sail artisan migrate
```

--------------------------------------------------------------------------------

## Install Breeze

1. Installing Breeze via Composer and sail
```
$ ./vendor/bin/sail composer require laravel/breeze
$ ./vendor/bin/sail artisan breeze:install vue --dark
```
