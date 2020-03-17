FROM bkuhl/laravel-fpm-nginx:latest

RUN apk update
RUN apk add libzip-dev libpng-dev
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl sockets json bcmath gd
# # RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
# RUN docker-php-ext-install gd

WORKDIR /var/www/html

USER www-data

# Copy the application files to the container
ADD --chown=www-data:www-data  ./masterCODE /var/www/html

    # production-ready dependencies
RUN composer install --no-interaction --optimize-autoloader --no-dev --prefer-dist \
    # keep the container light weight
    && rm -rf /home/www-data/.composer/cache

# RUN php artisan key:generate --force

# RUN php artisan jwt-secret -f
    # && compile front-end assets
    # && yarn install \
    # && yarn run production \
    # && yarn cache clean
USER root