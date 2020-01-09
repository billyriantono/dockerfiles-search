FROM ubuntu:16.04

LABEL maintainer="dev@crowdlinker.com"

# Remove debconf errors
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

# Install defaults
RUN apt-get update && \
  apt-get install -y --no-install-recommends --no-install-suggests \
  mc \
  zip \
  curl \
  nano \
  nginx \
  unzip \
  gettext \
  git-core \
  apt-utils \
  libssl-dev \
  zlib1g-dev \
  libpng-dev \
  supervisor \
  libjpeg-dev \
  libwebp-dev \
  libxml2-dev \
  mysql-client \
  libmcrypt-dev \
  build-essential \
  ca-certificates \
  libfreetype6-dev \
  libmagickwand-dev \
  apt-transport-https \
  software-properties-common \
  python-software-properties

# Install php7.2
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php -y && \
  apt-get update && \
  apt-get install -y --no-install-recommends --no-install-suggests \
  php7.2-fpm \
  php7.2-cli \
  php-pear \
  php-mcrypt \
  php7.2-gd \
  php7.2-gmp \
  php7.2-zip \
  php7.2-xml \
  php7.2-cli \
  php7.2-pdo \
  php7.2-ldap \
  php7.2-json \
  php7.2-ldap \
  php7.2-curl \
  php7.2-amqp \
  php7.2-intl \
  php7.2-soap \
  php7.2-iconv \
  php7.2-mysql \
  php7.2-redis \
  php7.2-xmlrpc \
  php7.2-mysqli \
  php7.2-bcmath \
  php7.2-mongodb \
  php7.2-sockets \
  php7.2-mbstring \
  php7.2-fileinfo \
  php7.2-simplexml \
  php7.2-xdebug

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --install-dir=bin --filename=composer \
  && php -r "unlink('composer-setup.php');"

# Install node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && \
  apt-get update && apt-get install nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && apt-get install -y --no-install-recommends yarn

# Set timezone - America/Toronto
RUN cp /usr/share/zoneinfo/America/Toronto /etc/localtime

# Forward requests & error logs
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log \
  && ln -sf /dev/stderr /var/log/php7.2-fpm.log

# Set nginx configuration
COPY ./nginx/default.conf /etc/nginx/sites-enabled/default.conf
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

# Set php configuration
COPY ./php/php.ini /etc/php/7.2/cli/php.ini
COPY ./php/php.ini /etc/php/7.2/fpm/php.ini

# For starting php-fpm with supervisord
RUN sed -i 's/;daemonize = yes/daemonize = no/g' /etc/php/7.2/fpm/php-fpm.conf

# Copy supervisor configuration
COPY ./supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Create directories for php
RUN mkdir -p /var/run/php
RUN mkdir -p /var/log/php-fpm

# Add colors to bash commands
COPY .docker-prompt /etc/.docker-prompt
RUN echo '. /etc/.docker-prompt' >> /etc/bash.bashrc\
  && echo '. /etc/.docker-prompt' >> /root/.bashrc

# Set working directory
WORKDIR /usr/share/nginx/html

# Expose port
EXPOSE 80 3306 2525 6379

# Copy php index file
COPY ./html/index.php /usr/share/nginx/html/index.php

# Create project directory
RUN mkdir -p /usr/share/nginx/html/project

# Set project directory as working directory
WORKDIR /usr/share/nginx/html/project

# Start everything
COPY ./entrypoint.sh /
ENTRYPOINT [ "sh", "/entrypoint.sh" ]
