FROM alpine

COPY www /var/www

RUN apk update \
    && apk add php composer \
    && cd /var/www \
    && composer install -o --no-dev \
    && apk del composer \
    && rm -rf /var/cache/apk/*

ENTRYPOINT php -S 0.0.0.0:80 -t /var/www
