FROM php:7.2-fpm-stretch

MAINTAINER "Jeremy CURNY" <jeremy.curny.pro@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
  && apt-get install -y \
    libfreetype6-dev libicu-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libxml2-dev libxslt-dev \
    ack-grep bash curl git jq mysql-client nano python3-pip unzip zip \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove

RUN \
  pecl install mcrypt xdebug

RUN \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ \
  && docker-php-ext-install gd

RUN \
  docker-php-ext-enable mcrypt

RUN \
  docker-php-ext-install bcmath mysqli intl opcache pcntl pdo_mysql soap sockets xsl zip

RUN \
  curl -o libsodium.tar.gz https://download.libsodium.org/libsodium/releases/libsodium-1.0.18.tar.gz \
    && tar xfvz libsodium.tar.gz \
    && rm libsodium.tar.gz \
    && cd libsodium-1.0.18 \
    && ./configure \
    && make && make install \
    && pecl install -f libsodium

RUN \
  echo "memory_limit = 1024M" > /usr/local/etc/php/conf.d/memory-limit.ini

RUN \
  curl -sLS -o /usr/local/bin/composer https://getcomposer.org/composer.phar \
  && chmod +x /usr/local/bin/composer

RUN \
  pip3 install awscli --upgrade

ENV APP_PATH /var/www/html
ENV ARTIFACT_PATH /root/artifact
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV MAGENTO_PATH /var/www/html
ENV MAGENTO_PATH_BIN /var/www/html/bin/magento
ENV MAGENTO_PUB_KEY 6c7c3956d991c6459bcbf6d0d977514f
ENV MAGENTO_PRI_KEY 2319f30adac6169a5c30ad2cb564d177
ENV MAGENTO_PROJECT magento/project-community-edition
ENV TMP_DECK /tmp/deck

RUN \
  rm -rf $APP_PATH $ARTIFACT_PATH $TMP_DECK \
  && mkdir -p $APP_PATH $ARTIFACT_PATH $TMP_DECK

COPY docker-php-magento2-entrypoint docker-php-magento2-ext-* /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-php-magento2-*

RUN composer global config --auth http-basic.repo.magento.com $MAGENTO_PUB_KEY $MAGENTO_PRI_KEY

ENTRYPOINT ["docker-php-magento2-entrypoint"]
EXPOSE 9000
CMD ["php-fpm"]
