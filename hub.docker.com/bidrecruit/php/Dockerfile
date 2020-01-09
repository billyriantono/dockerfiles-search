FROM alpine:latest

# Update existing packages
RUN apk update && apk upgrade

# Core utils
RUN apk add curl bash unzip

# PHP 7
RUN apk add \
    php7 \
    php7-zlib \
    php7-json \
    php7-ctype \
    php7-curl \
    php7-session \
    php7-dom \
    php7-openssl \
    php7-mbstring \
    php7-phar \
    php7-pdo \
    php7-tokenizer \
    php7-xml \
    php7-xmlwriter \
    php7-zip \
    php7-mysqli \
    php7-pdo_mysql \
	php7-gd \
    php7-simplexml \
    php7-imagick \
    php7-fileinfo \
    php7-xmlreader \
    php7-xdebug \
    php7-redis

# Add Composer and Prestissimo
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN composer global require hirak/prestissimo

# Add project root
WORKDIR /var/www

# Start PHP server at port 8000
CMD php -S 0.0.0.0:8080