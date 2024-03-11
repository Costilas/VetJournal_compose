FROM php:8.1-fpm

# Сделать Composer доступным внутри контейнера
COPY ./docker/php-fpm/conf.d /usr/local/etc/php/conf.d
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Обновление пакетов и установка необходимых зависимостей
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y libyaml-dev autoconf make g++ \
    && pecl install yaml-2.2.2 \
    && docker-php-ext-install mysqli pdo pdo_mysql bcmath \
    && docker-php-ext-enable yaml

# Копирование конфигурации PHP
RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini

# Установка Xdebug
RUN pecl install xdebug-3.1.2 \
    && docker-php-ext-enable xdebug

# Создание файла лога для Xdebug и установка прав
RUN touch /var/log/xdebug.log && chmod 777 /var/log/xdebug.log

WORKDIR /app





