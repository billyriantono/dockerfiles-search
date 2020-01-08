FROM iwyg/php:7.1-cli

ENV PHP_XDEBUG_VERSION master
ENV XDEBUG_HOST=172.17.0.1

RUN set -xe \
  && apk add --no-cache --virtual .build-deps \
  $PHPIZE_DEPS \
  && git clone --branch ${PHP_XDEBUG_VERSION} https://github.com/xdebug/xdebug /tmp/php-xdebug \
  && cd /tmp/php-xdebug \
  && phpize  \
  && ./configure  \
  && make  \
  && make install \
  && make test \
  && apk del .build-deps \
  && rm -rf /tmp/*

COPY config/xdebug-cli.ini $PHP_INI_DIR/conf.d/
