# adapted from https://github.com/alterway/docker-php/blob/f1695cc9bb099fcbc2ec5dc104c12b2fa3bb0daa/5.4-cli/Dockerfile

FROM php:5.4-cli

# git and unzip are necessary for Composer, libicu-dev is necessary for internationalization
RUN apt-get update && \
    apt-get install -y \
        git \
        unzip \
        libicu-dev && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/

RUN docker-php-ext-install intl && \
    docker-php-ext-configure intl && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install pcntl && \
    docker-php-ext-install pdo_mysql

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
# add plugin then remove cache
RUN composer global require "hirak/prestissimo:^0.3" && \
    rm -rf /root/.composer/cache

# avoid error “Warning: date_default_timezone_get(): It is not safe to rely on the system's timezone settings.”
# source: https://stackoverflow.com/questions/45587214/configure-timezone-in-dockerized-nginx-php-fpm/45587945#45587945
RUN printf '[PHP]\ndate.timezone = "Europe/Paris"\n' > /usr/local/etc/php/conf.d/tzone.ini

WORKDIR /app
