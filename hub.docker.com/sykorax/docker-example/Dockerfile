FROM php:7.2.5-fpm-alpine3.7 as dev

LABEL maintainer="Forgács Bence <sykorax93@gmail.com>"

# -------------------------------------------------------------
# PHP
ENV PHP_VERSION "7.2"

# -------------------------------------------------------------
# Composer
# Updation: https://getcomposer.org/download/
ENV COMPOSER_DOWNLOAD_URL "https://getcomposer.org/installer"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /home/.composer

RUN apk add --update \
        openssl \
        zip \
        unzip \
        git \
        curl \
    && curl --silent https://getcomposer.org/installer | php \
    && docker-php-source extract \
    #&& docker-php-ext-enable \
    && docker-php-source delete
    #&& docker-php-ext-install pdo pdo_mysql

# Copy the application into the container
#COPY . /var/www
COPY . /var/www

# Copy and setup startup file
COPY start.sh /usr/local/bin/start
RUN chown -R www-data:www-data /var/www \
    && chmod +x /usr/local/bin/start

# Run startup bash script
ENTRYPOINT ["/usr/local/bin/start"]

USER www-data
WORKDIR /var/www
