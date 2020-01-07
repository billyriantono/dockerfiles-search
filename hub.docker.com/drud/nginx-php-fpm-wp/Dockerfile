FROM drud/nginx-php-fpm:latest

ENV TERM xterm

RUN apk update && apk add less

ADD files/ /
WORKDIR /var/www/html/docroot
