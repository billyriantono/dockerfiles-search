FROM accelys/php:7.2-fpm

#ENV DRUPAL_VERSION=8.7.1
ENV DRUPAL_PROJECT=drupal-composer/drupal-project:8.x-dev
ENV DRUPAL_ROOT=web
ENV DRUPAL_PROFILE=standard
ENV DRUPAL_LANGCODE=en

COPY quickstart.sh /usr/local/bin/drupal-quickstart

RUN mkdir /app
WORKDIR /app

EXPOSE 8028

CMD drupal-quickstart