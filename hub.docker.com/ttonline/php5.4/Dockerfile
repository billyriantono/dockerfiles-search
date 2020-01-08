FROM php:5.4-apache

RUN useradd -ms /bin/bash composer

# Set correct timezone
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    ant \
    git \
    libxml2-dev \
    php-soap \
    php5-curl \
    php5-mcrypt \
    php5-sqlite \
    php5-xdebug \
    zip \
&& docker-php-ext-install soap \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*
