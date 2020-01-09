FROM ubuntu:16.04

MAINTAINER filipe cristian (ambiente PHP / nginx)

RUN apt-get update

RUN apt-get install -y iputils-ping \
    software-properties-common \ 
    python-software-properties \ 
    curl \
    composer \
    vim

RUN apt-get update

RUN mkdir /app

RUN apt-get install nginx -y && \ 
    apt-get update

RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php

RUN apt-get update

RUN apt-get install -y php7.2-fpm php7.2-cli php7.2-fpm php7.2-mysql \
    php7.2-curl php-memcached  php7.2-dev php7.2-sqlite3 php7.2-mbstring \ 
    php7.2-gd php7.2-json php7.2-xmlrpc php7.2-xml php7.2-zip php7.2-mongodb php-xdebug

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get install -y nodejs

RUN ln -sf /dev/stdout /var/log/nginx/access.log

RUN ln -sf /dev/stderr /var/log/nginx/error.log

ADD ./php/php.ini /etc/php/7.2/fpm

ADD ./nginx/default /etc/nginx/sites-available 

COPY ./start.sh /

RUN chmod +x /start.sh

WORKDIR "/app"

ENTRYPOINT ["/start.sh"]
