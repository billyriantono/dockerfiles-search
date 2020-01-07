FROM ubuntu:16.04

# set some environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV USER_ID 1000

# upgrade the container
RUN apt-get update && apt-get install -y software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update && apt-get upgrade -y

# install some prerequisites
RUN apt-get install -y curl \
    git \
    nano \
    wget
    
# setup bash
COPY config/.bash_aliases /root

# install nginx
RUN apt-get install -y nginx
COPY config/nginx/sites/default /etc/nginx/sites-available/default
COPY config/nginx/nginx.conf /etc/nginx/nginx.conf

# install php
RUN apt-get install -y php7.1 php7.1-fpm php7.1-cli php7.1-dev php7.1-pgsql php7.1-sqlite3 php7.1-gd \
    php7.1-apcu php7.1-curl php7.1-mcrypt php7.1-imap php7.1-mysql php7.1-readline php7.1-xdebug php7.1-common \
    php7.1-mbstring php7.1-xml php7.1-zip

ADD ./config/php/local.ini /etc/php/7.1/fpm/php.ini

RUN phpenmod mcrypt && \
    mkdir -p /run/php/ && chown -Rf www-data.www-data /run/php

# install sqlite 
RUN apt-get install -y sqlite3 libsqlite3-dev

# install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    printf "\nPATH=\"~/.composer/vendor/bin:\$PATH\"\n" | tee -a ~/.bashrc

# install nodejs
RUN apt-get install -y nodejs

# install redis 
RUN apt-get install -y redis-server

# install beanstalkd
RUN apt-get install -y beanstalkd && \
    sed -i "s/BEANSTALKD_LISTEN_ADDR.*/BEANSTALKD_LISTEN_ADDR=0.0.0.0/" /etc/default/beanstalkd && \
    sed -i "s/#START=yes/START=yes/" /etc/default/beanstalkd && \
    /etc/init.d/beanstalkd start

# install supervisor
RUN apt-get install -y supervisor && \
    mkdir -p /var/log/supervisor
COPY config/supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
VOLUME ["/var/log/supervisor"]

# clean up our mess
RUN apt-get autoremove -y && \
    apt-get clean && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/*

# expose ports
EXPOSE 80 443 6379

COPY config/startup.sh /
RUN chmod +x /startup.sh

# set container entrypoints
ENTRYPOINT ["/startup.sh"]

WORKDIR /var/www
