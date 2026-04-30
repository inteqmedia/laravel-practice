FROM php:8.3-fpm

RUN apt-get update && apt-get install -y \
    unzip curl git libpng-dev libonig-dev libxml2-dev zip

RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY src/ /var/www

RUN composer install || true

EXPOSE 9000

CMD ["php-fpm"]