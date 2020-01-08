FROM php:7-alpine3.8

RUN curl -O -L https://github.com/mglaman/drupal-check/releases/download/1.0.5/drupal-check.phar \
  && chmod +x drupal-check.phar \
  && mv drupal-check.phar /usr/local/bin/drupal-check

WORKDIR /app