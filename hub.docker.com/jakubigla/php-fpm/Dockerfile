FROM alpine:3.1

MAINTAINER Jakub Igla <jakub.igla@gmail.com>

RUN apk --update add php-fpm php-curl php-json php-gd php-intl php-pdo php-pdo_mysql php-ctype php-xml php-dom nano

COPY conf/php-fpm.conf /etc/php/

EXPOSE 9000

CMD ["php-fpm"]