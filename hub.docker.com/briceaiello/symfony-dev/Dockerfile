FROM mykiwi/symfony-base:7.2-fpm
MAINTAINER Brice AIELLO <brice.aiello@me.com>

RUN apt-get update && \ 
    apt-get install -y --no-install-recommends \
    libzip-dev \
    zip \
    curl \
    ruby-full

RUN docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip

RUN gem install dpl
