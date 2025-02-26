FROM php:8.3.17-fpm-alpine3.20

ARG HOST_UID=1000
ENV HOST_UID=$HOST_UID

RUN apk add zlib-dev libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
        icu-dev libpq postgresql-dev autoconf gcc g++ make \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install gd intl bcmath opcache pdo pdo_pgsql \
	&& apk add --update linux-headers \
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug \
	&& apk add --no-cache shadow && usermod -u "${HOST_UID}" www-data && groupmod -g "${HOST_UID}" www-data

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

USER www-data

WORKDIR /var/www/html

