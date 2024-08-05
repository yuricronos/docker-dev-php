FROM php:8.3-fpm-alpine

RUN apk update 

# zip and gd extension
RUN apk add libzip-dev zip unzip libpng-dev libjpeg-turbo-dev freetype-dev oniguruma-dev
RUN docker-php-ext-configure zip
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) zip gd

# posgresql driver
RUN apk add postgresql-dev libzip-dev
RUN docker-php-ext-install pdo pdo_pgsql pgsql

# enable opcache
RUN docker-php-ext-enable opcache

RUN apk add --no-cache \
       $PHPIZE_DEPS \
       linux-headers \
       && pecl install xdebug \
       && docker-php-ext-enable xdebug \
       && apk del $PHPIZE_DEPS linux-headers

# COPY docker/php/config/*.ini /usr/local/etc/php/conf.d/

EXPOSE 9000

CMD ["php-fpm"]