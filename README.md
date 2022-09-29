# Travellist - Laravel Demo App

This is a Laravel 6 demo application to support our Laravel guides.

```
docker-compose build app
docker-compose up -d
docker ps
docker-compose exec -T app ls -la
docker-compose exec -T app rm -rf vendor composer.lock
docker-compose exec -T app composer install
docker-compose exec -T app composer update
docker-compose exec -T app php artisan key:generate
docker-compose exec -T app php artisan migrate

```
### Useful Link

```
https://www.digitalocean.com/community/tutorials/how-to-install-and-set-up-laravel-with-docker-compose-on-ubuntu-22-04

```
