# Laravel Portfoilo Management

Welcome to the Laravel Portfoilo Management Web Application! Our goal is to offer a simple way of managing financial portfolios.

## How to use via Docker

- Clone the repository with __git clone__
- Copy __.env.docker__ file to __.env__ and edit database credentials there
- Install application composer dependencies
`docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    composer install --ignore-platform-reqs`
- Run __php artisan key:generate__
- Run __php artisan migrate --seed__ (it has some seeded data for your testing)
- That's it: launch the main URL.
- You can login to adminpanel by going go `/login` URL and login with credentials __admin@admin.com__ - __password__
- For other users, doctors/directors, their email is in `users.email` field, and password is __password__


## License

Basically, feel free to use and re-use any way you want.


## Instructions
