FROM phusion/baseimage:0.11

RUN ls /

# Ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

ENV HOME /root

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]

# Nginx-PHP Installation
RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y vim curl wget build-essential software-properties-common
RUN add-apt-repository -y ppa:ondrej/php
RUN add-apt-repository -y ppa:nginx/stable
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get update

RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y php7.3-cli php7.3-fpm php7.3-mysql php7.3-curl \
    php7.3-gd php7.3-intl php7.3-imap php7.3-tidy php7.3-memcache php7.3-sqlite3 \
    php7.3-redis php7.3-mbstring php7.3-dom php7.3-xml php7.3-zip php7.3-bcmath php7.3-soap

RUN phpenmod mcrypt

RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y nginx nodejs

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir /run/php

RUN sed -i "/;clear_env = .*/c\clear_env = no" /etc/php/7.3/fpm/pool.d/www.conf \
    && sed -i "/;catch_workers_output = .*/c\catch_workers_output = yes" /etc/php/7.3/fpm/pool.d/www.conf \
    && sed -i "/pid = .*/c\;pid = /run/php/php7.3-fpm.pid" /etc/php/7.3/fpm/php-fpm.conf \
    && sed -i "/;daemonize = .*/c\daemonize = no" /etc/php/7.3/fpm/php-fpm.conf \
    && sed -i "/session\.cache_limiter = .*/c\session.cache_limiter = " /etc/php/7.3/fpm/php.ini

ADD utils/default   /etc/nginx/sites-available/default
RUN mkdir           /etc/service/nginx
ADD utils/nginx.sh  /etc/service/nginx/run
RUN chmod +x        /etc/service/nginx/run
RUN mkdir           /etc/service/phpfpm
ADD utils/phpfpm.sh /etc/service/phpfpm/run
RUN chmod +x        /etc/service/phpfpm/run

# install composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# install yarn
RUN npm i -g yarn

# aliases
RUN echo 'alias art="php artisan"' >> ~/.bashrc
RUN echo "alias phpunit='./vendor/bin/phpunit'" >> ~/.bashrc

# EXPOSE 80 443
# VOLUME ["/app"]

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
