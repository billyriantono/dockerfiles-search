FROM php:7.2-cli-alpine
MAINTAINER Asaf Ohayon <asaf@sysbind.co.il>
RUN apk add --update libzip && apk add --virtual build-deps libzip-dev
ADD . /
RUN curl -s http://getcomposer.org/installer | php && ./composer.phar install
RUN apk del build-deps
ENTRYPOINT /main.php
