FROM phpmyadmin/phpmyadmin:4.7.3-1

MAINTAINER Jeremy Crombez <jeremy.crombez [at] kibatic.com>

ADD etc/phpmyadmin/config.user.inc.php /etc/phpmyadmin/config.user.inc.php

ENV PMA_DOCKER_DISCOVERY_VERSION=698abbfa6dae81054d54de03c4dd558bc080a65e

RUN apk update && apk upgrade && apk add --update --no-cache \
    wget \
    curl \
    git \
  	php7-phar \
    php7-curl \
    php7-openssl

RUN curl -sS https://getcomposer.org/installer | php7 -- --install-dir=/usr/bin --filename=composer

RUN wget https://github.com/kibatic/phpmyadmin-docker-discovery/archive/$PMA_DOCKER_DISCOVERY_VERSION.zip && \
    unzip /$PMA_DOCKER_DISCOVERY_VERSION.zip && \
    mkdir /etc/phpmyadmin/discovery && \
    mv /phpmyadmin-docker-discovery-*/* /etc/phpmyadmin/discovery && \
    rm /$PMA_DOCKER_DISCOVERY_VERSION.zip

RUN cd /etc/phpmyadmin/discovery &&\
    php7 /usr/bin/composer install

RUN sed -i 's/nobody/root/g' /etc/php-fpm.conf
RUN sed -i 's/nobody/root/g' /etc/nginx.conf
RUN sed -i 's/nobody/root/g' /etc/supervisor.d/php.ini
RUN sed -i 's/--nodaemonize/--nodaemonize --allow-to-run-as-root/g' /etc/supervisor.d/php.ini

RUN apk add --update --no-cache bash
