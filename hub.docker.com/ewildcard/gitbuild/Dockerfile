FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "Europe/Berlin" | tee /etc/timezone

RUN apt-get update \
    && apt-get install -y \
     curl \
     git \
     zip \
     tzdata

RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:ondrej/php

RUN apt-get update \
    && apt-get install -y \
    php7.0 \
    php7.0-dom \
    php7.0-xml \
    php7.0-mbstring \
    nodejs \
    npm \
    ruby

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN gem install sass -v 3.4.19

RUN /usr/bin/npm install -g grunt-cli@1.3.2