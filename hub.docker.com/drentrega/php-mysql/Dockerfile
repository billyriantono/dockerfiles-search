FROM php:7.2-fpm-stretch

LABEL vendor="Dr.Entrega" \
      maintainer="Dr.Entrega <technology+docker@drentrega.com>" \
      image="php" \
      tag="7.2-fpm-stretch"

RUN apt-get update -yq \
  && apt-get upgrade -yq \
  && apt-get install libmcrypt-dev mysql-client libmagickwand-dev -yq --no-install-recommends \
  && pecl install imagick mcrypt-1.0.1 \
  && docker-php-ext-enable imagick mcrypt \
  && docker-php-ext-install pdo_mysql \
  && apt-get clean -yq \
  && apt-get autoremove -yq

# This dockerfile was auto-generated at 2019-04-16T19:00:24-03:00.

# In case of security branches, please contact technology+security@drentrega.com.