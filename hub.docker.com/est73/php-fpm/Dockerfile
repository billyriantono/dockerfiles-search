FROM ubuntu:trusty

MAINTAINER est73 <brian@est73.com>

RUN add-apt-repository -y ppa:ondrej/php-7.0
RUN apt-get update
RUN apt-get install -f -y php7.0-cli php7.0-common php7.0-curl php7.0-dev php7.0-fpm php7.0-gd php7.0-json php7.0-mcrypt php7.0-mysql php7.0-opcache php-pear

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# forward error log to docker log collector
# RUN ln -sf /dev/stderr /var/log/php7.0-fpm.log

# add the custom config file
# COPY www.conf /etc/php/7.0/fpm/pool.d/www.conf

EXPOSE 9000