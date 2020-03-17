FROM bkuhl/laravel-fpm-nginx:latest

RUN apk update
RUN apk add libzip-dev libpng-dev
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl sockets json bcmath gd

WORKDIR /var/www/html

USER www-data

ADD --chown=www-data:www-data  ./subCODE /var/www/html

RUN composer install --no-interaction --optimize-autoloader --no-dev --prefer-dist \
    && rm -rf /home/www-data/.composer/cache

RUN yarn install \
    && yarn run production \
    && yarn cache clean
USER root