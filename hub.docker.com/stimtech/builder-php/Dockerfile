FROM php:7.2-fpm-alpine

ARG BUILD_DATE
ARG VCS_REF

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV PHALCON_VERSION=3.4.5
ENV PHALCON_EXT_PATH=php7/64bits

LABEL Maintainer="Tobias Sjösten <tobias.sjosten@stim.se>" \
      Description="PHP 7.2 image with batteries included" \
      org.label-schema.name="stimtech/builder-php" \
      org.label-schema.description="PHP 7.2 image with batteries included" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://bitbucket.org/stimtech/docker-builder-php" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0"

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]
RUN set -ex \
    && apk update \
    && apk add --no-cache alpine-sdk=1.0-r0 autoconf=2.69-r2 git=2.22.0-r0 icu-dev=64.2-r0 libpng-dev=1.6.37-r1 \
    libxml2-dev=2.9.9-r2 openssh-client=8.1_p1-r0 \
    && pecl install xdebug ast \
    && docker-php-ext-enable xdebug ast \
    && curl -sSL "https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION}" | tar -xz \
    && docker-php-ext-install -j"$(nproc)" gd intl soap zip "${PWD}/cphalcon-${PHALCON_VERSION}/build/${PHALCON_EXT_PATH}" \
    && rm -r "${PWD}/cphalcon-${PHALCON_VERSION}" \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && curl -sSo /usr/local/bin/phpcov https://phar.phpunit.de/phpcov.phar \
    && chmod +x /usr/local/bin/phpcov \
    && apk del alpine-sdk autoconf \
    && rm -rf /tmp/*
