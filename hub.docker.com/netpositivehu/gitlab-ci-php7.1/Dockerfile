FROM debian:jessie

MAINTAINER <info@netpositive.hu>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
    wget \
    curl \
    lsb-release \
    apt-transport-https \
    ca-certificates

RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/sury.list
RUN wget -O /etc/apt/trusted.gpg.d/sury.gpg https://packages.sury.org/php/apt.gpg
RUN apt-get update

# PHP
RUN apt-get install -y \
    git \
    php7.1-cli \
    php7.1-json \
    php7.1-curl \
    php7.1-mysql \
    php7.1-gd \
    php7.1-xml \
    php7.1-zip \
    php7.1-memcached \
    php7.1-mbstring \
    php7.1-bcmath \
    php7.1-soap \
    php-intl

# Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

