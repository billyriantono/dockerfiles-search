FROM php:7.2.2-fpm-alpine3.7

RUN apk update && apk --no-cache add --virtual .build-deps $PHPIZE_DEPS \
  && apk --no-cache add --virtual .ext-deps libmcrypt-dev freetype-dev libxml2-dev \
  git msmtp bash openssl-dev pkgconfig icu-dev openssh curl alpine-sdk nasm \
  automake autoconf build-base zlib zlib-dev libpng libpng-dev libjpeg-turbo \
  libjpeg-turbo-dev libwebp libwebp-dev nodejs nodejs-npm mysql-client gmp gmp-dev \
  && docker-php-source extract \
  && docker-php-ext-configure intl \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \
                                   --with-png-dir=/usr/include/ \
                                   --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd mysqli pdo pdo_mysql zip opcache intl soap gmp bcmath \
  && pecl install redis \
  && docker-php-ext-enable redis \
  && docker-php-source delete \
  && npm install --global npm@5 \
  && npm install --global yarn \
  && apk del .build-deps

RUN curl -sS https://getcomposer.org/installer | php \
  && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/html

LABEL maintainer="Jon Bowes <jon@jbxonline.net>"

COPY entrypoint.sh /usr/local/bin/
RUN chmod u+x /usr/local/bin/entrypoint.sh

CMD bash -c "/usr/local/bin/entrypoint.sh"

