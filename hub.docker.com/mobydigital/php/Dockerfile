FROM php:7.1-fpm-alpine

MAINTAINER eteplus <eteplus@163.com>

RUN docker-php-source extract && \
  apk add --no-cache --virtual .build-dependencies autoconf g++ make \
  && apk add --no-cache zlib-dev \
  libxslt-dev libmcrypt-dev icu-dev libpng-dev curl-dev \
  jpeg-dev freetype-dev && \
  pecl install redis && \
  docker-php-ext-enable redis && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install opcache \
  curl \
  bcmath \
  mcrypt \
  intl \
  hash \
  xsl \
  zip \
  mysqli \
  pdo \
  pdo_mysql \
  mbstring \
  iconv \
  json \
  xml \
  soap \
  simplexml \
  gd \
  && docker-php-source delete \
  && apk --no-cache del .build-dependencies

RUN mkdir /root/.composer \
    && curl -s https://configs-devops-mobydigital.netlify.com/magento2/php-fpm/php-fpm.conf > /usr/local/etc/php-fpm.conf \
    && curl -s https://configs-devops-mobydigital.netlify.com/magento2/php-fpm/php.ini > /usr/local/etc/php/php.ini \
    && curl -s https://configs-devops-mobydigital.netlify.com/magento2/composer_auth.json > /root/.composer/auth.json

WORKDIR /var/www/html
CMD [ "php-fpm", "-F" ]
