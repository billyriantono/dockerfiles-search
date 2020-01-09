FROM alpine:3.8

RUN set -xe \
    && apk add --update --no-cache \
    php7 

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
