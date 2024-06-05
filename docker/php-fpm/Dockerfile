FROM php:8.3-fpm

COPY ./docker/php-fpm/conf.d /usr/local/etc/php/
COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN mkdir -p /var/log/php-fpm \
    && touch /var/log/php-fpm/xdebug.log \
    && touch /var/log/php-fpm/error.log \
    && chmod -R 777 /var/log/php-fpm

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
        autoconf \
        pkg-config \
        libcurl4-openssl-dev \
        libxml2-dev \
        libicu-dev \
        libonig-dev \
        libzip-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libxslt1-dev \
        libc-client-dev \
        libkrb5-dev \
        libtidy-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
        ctype \
        curl \
        dom \
        fileinfo \
        filter \
        mbstring \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        session \
        xml \
        zip \
        gd \
        intl

RUN pecl install xdebug-3.3.0 \
    && docker-php-ext-enable xdebug

WORKDIR /var/www/html/app