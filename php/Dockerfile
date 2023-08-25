FROM php:8.2-fpm-alpine

RUN docker-php-ext-install pdo pdo_mysql

# Allow super user 
ENV COMPOSER_ALLOW_SUPERUSER=1

# Obtain composer userng multi-stage build
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

COPY ./app/composer.* ./

# Install
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

# Copy application files to the working directory
COPY ./app .

# Run composer dump-autoload --optimize
RUN composer dump-autoload --optimize