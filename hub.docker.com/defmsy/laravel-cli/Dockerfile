FROM composer/composer

RUN composer global require "laravel/installer"

RUN mkdir -p /app

WORKDIR /app

ENTRYPOINT ["laravel"]