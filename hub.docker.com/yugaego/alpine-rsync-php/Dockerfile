FROM alpine:latest

RUN apk add --no-cache openssh-client bash php php7-json php7-phar php7-iconv php7-openssl curl rsync ca-certificates  && rm -rf /var/cache/apk/*
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN php --version
RUN composer --version