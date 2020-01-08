FROM ubuntu:latest
MAINTAINER Jonathon Suggs <jsuggs@gmail.com>

RUN apt-get update \
  && apt-get install -y \
    curl \
    php5 \
    php5-json \
    php5-readline \
    php-codesniffer \
    php-doc \
  && apt-get clean

RUN /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php
RUN /bin/mv composer.phar /usr/local/bin/composer

RUN mkdir /code
WORKDIR /code
COPY composer.json /code/
COPY test.php /code/

RUN composer install
