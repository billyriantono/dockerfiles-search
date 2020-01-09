FROM php:7.3-fpm
MAINTAINER "Rus0 <andonid88@gmail.com>"

ENV PHP_EXTRA_CONFIGURE_ARGS="--enable-fpm --with-fpm-user=magento2 --with-fpm-group=magento2"
ENV NODE_VERSION="11.x"

RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -my wget gnupg

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 5072E1F5 
RUN echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-5.7" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    apt-utils \
    sudo \
    wget \
    unzip \
    cron \
    curl \
    libicu-dev \
    libxml2-dev libxslt1-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt4 \
    libcurl4-openssl-dev \
    git \
    vim \
    nano \
    openssh-server \
    supervisor \
    mysql-client \
    ocaml \
    expect \
    libsodium23 \
    libzip-dev


RUN curl -L https://github.com/bcpierce00/unison/archive/2.48.4.tar.gz | tar zxv -C /tmp && \
             cd /tmp/unison-2.48.4 && \
             sed -i -e 's/GLIBC_SUPPORT_INOTIFY 0/GLIBC_SUPPORT_INOTIFY 1/' src/fsmonitor/linux/inotify_stubs.c && \
             make && \
             cp src/unison src/unison-fsmonitor /usr/local/bin && \
             cd /root && rm -rf /tmp/unison-2.48.4

RUN apt-get update && apt-get install -y pkg-config patch
ADD https://git.archlinux.org/svntogit/packages.git/plain/trunk/freetype.patch?h=packages/php /tmp/freetype.patch
RUN docker-php-source extract; \
    cd /usr/src/php; \
    patch -p1 -i /tmp/freetype.patch; \
    rm /tmp/freetype.patch

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
RUN docker-php-ext-configure hash --with-mhash 
RUN docker-php-ext-install -j$(nproc) intl xsl gd zip pdo_mysql opcache soap pcntl bcmath json iconv
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 
RUN mkdir /var/run/sshd 
RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config 
RUN apt-get update && apt-get install -y apache2
RUN a2enmod rewrite 
RUN a2enmod proxy 
RUN a2enmod proxy_fcgi 
RUN rm -f /etc/apache2/sites-enabled/000-default.conf 
RUN useradd -m -d /home/magento2 -s /bin/bash magento2 && adduser magento2 sudo 
RUN touch /etc/sudoers.d/privacy 
RUN echo "Defaults        lecture = never" >> /etc/sudoers.d/privacy 
RUN mkdir /home/magento2/magento2 && mkdir /home/magento2/state 
RUN curl -sS https://accounts.magento.cloud/cli/installer -o /home/magento2/installer 
RUN rm -r /usr/local/etc/php-fpm.d/* 
RUN sed -i 's/www-data/magento2/g' /etc/apache2/envvars 
RUN pecl install xdebug-stable \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# PHP config
ADD conf/php.ini /usr/local/etc/php

# SSH config
COPY conf/sshd_config /etc/ssh/sshd_config
RUN chown magento2:magento2 /etc/ssh/ssh_config

# supervisord config
ADD conf/supervisord.conf /etc/supervisord.conf

# php-fpm config
ADD conf/php-fpm-magento2.conf /usr/local/etc/php-fpm.d/php-fpm-magento2.conf

# apache config
ADD conf/apache-default.conf /etc/apache2/sites-enabled/apache-default.conf

# unison script
ADD conf/.unison/magento2.prf /home/magento2/.unison/magento2.prf

ADD conf/unison.sh /usr/local/bin/unison.sh
ADD conf/entrypoint.sh /usr/local/bin/entrypoint.sh
ADD conf/check-unison.sh /usr/local/bin/check-unison.sh
RUN chmod +x /usr/local/bin/unison.sh && chmod +x /usr/local/bin/entrypoint.sh 
RUN chmod +x /usr/local/bin/check-unison.sh

ENV USE_SHARED_WEBROOT 1
ENV SHARED_CODE_PATH /var/www/html
ENV WEBROOT_PATH /var/www/html
ENV MAGENTO_ENABLE_SYNC_MARKER 0

## Python 2.7
RUN sudo apt-get install python2.7

## Node
WORKDIR /tmp/grunt
RUN curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | bash - \
    && apt-get update
RUN apt-get install -y build-essential nodejs 
RUN npm install -g express && npm install -g grunt-cli && npm install -g node-gyp

## Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list


RUN npm install -g yarn

# Delete user password to connect with ssh with empty password
RUN passwd magento2 -d

EXPOSE 80 22 5000 44100
WORKDIR /var/www/html

USER root

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
