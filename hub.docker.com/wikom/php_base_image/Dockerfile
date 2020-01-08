FROM php:5.6-apache

RUN apt-get -qq update \
    && apt-get -qq -y install libpq-dev \
    && apt-get -qq -y install postgresql-client \
    && docker-php-ext-install pdo_pgsql pgsql \
    && apt-get -qq -y install git \
    && apt-get -qq -y install zip \
    && apt-get -qq -y install unzip \
    && apt-get -qq -y install multitail \
    && apt-get -qq -y install sudo \
    && apt-get -qq -y install software-properties-common \
    && docker-php-ext-install zip