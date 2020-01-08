FROM ubuntu:xenial
MAINTAINER Alex Price <alexp@fishvision.com>
ENV DEBIAN_FRONTEND noninteractive

# Remove sh
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install packages
RUN apt-get update
RUN apt-get -y install wget \
    curl \
    git \
    zip \
    unzip \
    libxml2-dev \
    build-essential \
    libssl-dev \
    vim \
    nano \
    openssh-client \
    libreadline-gplv2-dev \
    libncursesw5-dev \
    libsqlite3-dev \
    tk-dev \
    libgdbm-dev \
    libc6-dev \
    libbz2-dev \
    software-properties-common

# Add repos
RUN add-apt-repository ppa:fkrull/deadsnakes
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update

# Install python
RUN apt-get install -y python2.7
RUN apt-get install -y python-pip
RUN pip install --upgrade pip

# Add ondrej php repo
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update

# Install PHP
RUN apt-get -y --allow-unauthenticated install \
    php5.6 \
    php5.6-cgi \
    php5.6-cli \
    php5.6-common \
    php5.6-curl \
    php5.6-dev \
    php5.6-gd \
    php5.6-gmp \
    php5.6-json \
    php5.6-ldap \
    php5.6-mysql \
    php5.6-odbc \
    php5.6-opcache \
    php5.6-pspell \
    php5.6-readline \
    php5.6-sqlite3 \
    php5.6-tidy \
    php5.6-xmlrpc \
    php5.6-xsl \
    php5.6-fpm \
    php5.6-intl \
    php5.6-mcrypt \
    php5.6-mbstring \
    php5.6-zip \
    php-xdebug

# Clean apt
RUN apt-get clean

# Install node
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash && \
    export NVM_DIR="/root/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm install 6.9 lts

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer creates=/usr/local/bin/composer
RUN php /usr/local/bin/composer global require "fxp/composer-asset-plugin:~1.1.1"
RUN php /usr/local/bin/composer global require "hirak/prestissimo:^0.3"

# Misc
RUN mkdir -p ~/.ssh
RUN [[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config
