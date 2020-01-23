FROM php:7.2-cli
MAINTAINER Dieter Provoost <dieter.provoost@marlon.be>

# https://github.com/puckel/docker-airflow/issues/182
RUN mkdir -p /usr/share/man/man1

RUN apt-get update && apt-get install -y \
    openjdk-8-jdk \
    git \
    unzip \
    ant \
    sqlite3 \
    curl \
    zlib1g-dev \
    libicu-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libxml2-dev

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Brussels /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install pdo pdo_mysql zip bcmath intl gd pcntl soap xml xmlrpc sockets

RUN apt-get autoremove -y

# PHP Developer configuration
ADD developer.ini /usr/local/etc/php/conf.d/developer.ini
