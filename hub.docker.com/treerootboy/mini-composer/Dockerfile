FROM alpine:latest

MAINTAINER LM <treerootboy@gmail.com>

RUN apk --update add php php-openssl php-json php-phar git \
    && rm -rf /var/cache/apk/* \
    && php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
    && php composer-setup.php --install-dir=bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer --version
    
WORKDIR /project
VOLUME /project
ENTRYPOINT ["composer"]
