FROM php:fpm

WORKDIR /app
ENV PATH=$PATH:/app/vendor/.bin

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /bin/composer

RUN apt-get update
RUN apt-get install -y \
  git \
  zlib1g-dev \
  ruby \
  ruby-dev

RUN docker-php-ext-install mbstring zip pdo_mysql

RUN gem install bundler