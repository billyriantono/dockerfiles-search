FROM php:7.4-fpm-alpine

ENV COMMIT_ID cb19f2aa3aeaa2006c0cd69a7ef011eb31463067
ENV COMPOSER_URL https://raw.githubusercontent.com/composer/getcomposer.org/${COMMIT_ID}/web/installer
ENV COMPOSER_VERSION 1.9.1

RUN curl --silent --fail --location --retry 3 --output /tmp/installer.php --url ${COMPOSER_URL} \
  ; php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
  ; rm -f /tmp/installer.php
