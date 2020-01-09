FROM richarvey/nginx-php-fpm:latest

RUN apk add --update make nano

COPY _docker/docker_hub/nginx.conf /etc/nginx/sites-enabled/default.conf
COPY _docker/php/php-ini-overrides.ini /etc/php/7.1/fpm/conf.d/99-overrides.ini

ADD . /application

WORKDIR "/application"

RUN composer install
RUN make chmod