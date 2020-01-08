FROM 4xxi/php:7.2.2-fpm-alpine3.7

RUN set -ex \
  && apk --no-cache add \
    postgresql-dev

# install pgsql ext
RUN docker-php-ext-install pdo pdo_pgsql
