# Version 0.0.1

FROM php:5.6.30-apache

MAINTAINER Ivano Masiero <info@ivanomasiero.com>

ENV TERM=xterm

RUN apt-get update && apt-get install -y \
    nano \
    git \
    zip \
    locate

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN updatedb

RUN a2enmod rewrite

RUN docker-php-ext-install pdo pdo_mysql mysqli

RUN apt-get update &&\
    apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git &&\
    rm -rf /var/lib/apt/lists/*

RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -

ENV PATH /usr/local/go/bin:$PATH

RUN go get github.com/mailhog/mhsendmail

RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/php.ini
