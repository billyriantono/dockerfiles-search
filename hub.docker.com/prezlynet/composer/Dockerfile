FROM composer:latest

RUN apk add --no-cache --virtual .build-deps \
  icu-dev \
  postgresql-dev \
  zlib-dev \
  libpng-dev \
  pcre-dev \
  gcc make \
  g++ \
  zlib-dev \
  autoconf

RUN docker-php-ext-install bcmath intl pgsql gd

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN apk del .build-deps \
    && rm -rf /var/cache/apk/*