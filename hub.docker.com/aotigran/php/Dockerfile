FROM php:fpm

# Adding PHP 7.0 repositories
RUN apt-get update
RUN apt-get install -y curl
RUN curl https://www.dotdeb.org/dotdeb.gpg | apt-key add -
RUN echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list
RUN echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list

# Installing PHP 7
RUN apt-get update
RUN apt-get install -y \
        git \
        php7.0 \
        php7.0-cli \
        php7.0-mcrypt \
        php7.0-gd \
        php7.0-xdebug \
        php7.0-curl \
        php7.0-mysql

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install openssl

RUN apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php 
RUN mv composer.phar /usr/local/bin/composer