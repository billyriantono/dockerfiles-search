FROM digitalkreativ/docker-php7.1-fpm
MAINTAINER Tom Sacré <github@digitalkreativ.com>

ADD ./install-composer.sh /var/install/

RUN ["chmod", "+x", "/var/install/install-composer.sh"]

RUN /var/install/install-composer.sh

WORKDIR /var/www/

CMD php-fpm

