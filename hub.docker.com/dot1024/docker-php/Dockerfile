# @VIA https://github.com/docker-library/php/blob/9bcb75e9dbd3a0ebafe3f825297724df30e3b254/7.2/stretch/fpm/Dockerfile
FROM php:7.2.25-fpm-stretch

ENV PHALCON_VERSION=3.4.5
ENV PHALCON_DEPS autoconf g++ make git 

ENV PHP_EXT_DEPS libmagickwand-dev

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends ${PHALCON_DEPS} ${PHP_EXT_DEPS}; \
    rm -rf /var/lib/apt/lists/*; \
    git clone -b v${PHALCON_VERSION} https://github.com/phalcon/cphalcon.git /usr/src/php/ext/phalcon; \
    cd /usr/src/php/ext/phalcon/build; \
    bash install --arch 64bits; \
    docker-php-ext-enable phalcon; \
    rm -rf /usr/src/php/ext/phalcon; \
    pecl update-channels; \
    docker-php-ext-install pdo_mysql; \
    docker-php-ext-enable pdo_mysql; \
    pecl install redis; \
    docker-php-ext-enable redis; \
    pecl install imagick; \
    docker-php-ext-enable imagick; \
    pecl install swoole; \
    docker-php-ext-enable swoole; \
    apt-get purge -y --auto-remove ${PHALCON_DEPS}; \
    rm -rf /tmp/* ~/.pearrc

EXPOSE 9000
CMD ["php-fpm"]