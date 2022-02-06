FROM php:8.1-fpm-bullseye
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

RUN apt-get update && apt-get -y install \
  git \
  unzip \
  libzip-dev \
  libicu-dev \
  libonig-dev

RUN docker-php-ext-install \
  intl \
  pdo_mysql \
  zip \
  bcmath

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# ----------------------------------------------
RUN apt-get update && apt-get -y install \
  vim \
  tree \
  net-tools
# ----------------------------------------------

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY ./docker/php/php-fpm.d/zzz-www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

WORKDIR /app
