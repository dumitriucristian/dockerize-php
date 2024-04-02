FROM php:8.1-fpm-alpine

RUN docker-php-ext-install pdo pdo_mysql

#allow super user
ENV COMPOSER_ALLOW_SUPERUSER=1

#use multystage to obtain composer
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

#cache composer
COPY ./app/composer.* ./ 

#install composer
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

#copy application files to the working directory
COPY ./app .

RUN composer dump-autoload --optimize