FROM php:7.1-fpm-alpine

ENV PATH "$PATH:/var/www/html/vendor/bin"

# Set up PHP with modules and ini settings for running WordPress
RUN apk update \
    && apk add --no-cache postgresql postgresql-dev \
    && docker-php-ext-install pdo pgsql pdo_pgsql \
    && echo "date.timezone=Europe/London" > /usr/local/etc/php/conf.d/zz-custom.ini \
    && echo "session.autostart=0" >> /usr/local/etc/php/conf.d/zz-custom.ini \
    && apk del postgresql-dev
