FROM phusion/baseimage

MAINTAINER viktor68 <apacheservices68@gmail.com>

RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash

RUN	\
	apt-get update \
	&&	apt-get -y upgrade \
	&&	apt-get update --fix-missing

RUN \
  	apt-get install -y \
	    php7.0 \
	    php-all-dev \
	    php7.0-bcmath \
	    php7.0-bz2 \
	    php7.0-cli \
	    php7.0-common \
	    php7.0-dev \
	    php7.0-fpm \
	    php7.0-ldap \
	    php7.0-gd \
	    php7.0-gmp \
	    php7.0-intl \
	    php7.0-json \
	    php7.0-mysql \
	    php7.0-mbstring \
	    php7.0-mcrypt \
	    php7.0-mysqlnd \
	    php7.0-opcache \
	    php7.0-odbc \
	    php7.0-pgsql \
	    php7.0-pdo \
	    php7.0-xml \
	    php7.0-phalcon \
	    php7.0-cli \
	    php7.0-zip \
	    php-igbinary \
	    php-redis \
	    php-imagick \
	    php-apcu \
	    php-amqp \
	    php-memcached \
	    php-xdebug \
	    php-geoip \
	    php-mongodb

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN service php7.0-fpm start

RUN \
  	apt-get install -y \
	    nodejs \
	    npm \
	    git

RUN \
  	apt-get install -y \
	    nginx-full \
	    supervisor

RUN apt-get clean
RUN apt-get autoclean

COPY build/.bashrc /root/.bashrc
COPY build/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY build/nginx.conf /etc/nginx/sites-enabled/default
COPY build/php.ini /etc/php/7.0/fpm/php.ini

ADD src /var/www/public/

EXPOSE 80 443
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]