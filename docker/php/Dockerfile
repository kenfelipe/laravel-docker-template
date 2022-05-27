FROM php:8.1-fpm-bullseye

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

RUN apt-get update && apt-get -y install \
  nodejs \
  npm

RUN apt-get -y install \
  libicu-dev \
  unzip \
  bash-completion \
  git \
  vim \
  tree \
  less \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install \
  intl \
  bcmath \
  pdo_mysql

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY ./docker/php/php-fpm.d/zzz-www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

WORKDIR /app
