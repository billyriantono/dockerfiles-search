FROM php:7.2.12-cli-stretch

RUN apt-get update
RUN apt-get install -y \
  curl \
  git \
  unzip
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php composer-setup.php

RUN mkdir -vp /app/kata
WORKDIR /app
RUN composer create-project symfony/skeleton kata
WORKDIR /app/kata
RUN composer require phpunit
RUN composer require server --dev

RUN php bin/phpunit
COPY entrypoint.sh /app/kata
RUN chmod +x /app/kata/entrypoint.sh
CMD ["/app/kata/bin/console", "server:run"]
ENTRYPOINT ["/app/kata/entrypoint.sh"]
