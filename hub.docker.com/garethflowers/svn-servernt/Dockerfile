FROM php:7-cli-alpine

RUN apk add --no-cache --no-progress supervisor

RUN docker-php-ext-install bcmath

ENTRYPOINT [ "/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf" ]