#
#--------------------------------------------------------------------------
# Yeti Workspace Base Image Setup
#--------------------------------------------------------------------------
#

FROM phusion/baseimage:latest

LABEL maintainer="Courtney Wilburn <courtney@cjwilburn.com>"

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN mkdir -p $HOME/.nvm
RUN mkdir -p /.nvm
RUN . ~/.bashrc

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

ENV MYSQL_ALLOW_EMPTY_PASSWORD=true
ENV MYSQL_PASS=""
ENV MYSQL_DATABASE=wp_tests
ENV MYSQL_HOST=127.0.0.1
ENV MYSQL_ROOT_HOST=%
ENV MYSQL_USER=root

ENV NVM_DIR=$HOME/.nvm
ENV NODE_VERSION=8.11.3

# Add the "PHP 7" ppa
RUN apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:ondrej/php

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#

# Install "PHP Extentions", "libraries", "Software's"
RUN apt-get update && \
    apt-get install -y --allow-downgrades --allow-remove-essential \
        --allow-change-held-packages \
        php7.0-cli \
        php7.0-common \
        php7.0-curl \
        php7.0-fpm \
        php7.0-imap \
        php7.0-intl \
        php7.0-json \
        php7.0-ldap \
        php7.0-xml \
        php7.0-mbstring \
        php7.0-mcrypt \
        php7.0-mysql \
        php7.0-opcache \
        php7.0-pgsql \
        php7.0-phpdbg \
        php7.0-pspell \
        php7.0-recode \
        php7.0-snmp \
        php7.0-sqlite \
        php7.0-sqlite3 \
        php7.0-tidy \
        php7.0-xml \
        php7.0-zip \
        php7.0-bcmath \
        php7.0-memcached \
        php7.0-gd \
        php7.0-dev \
        pkg-config \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        libsqlite3-dev \
        sqlite3 \
        git \
        git-svn \
        curl \
        debconf-utils \
        build-essential \
        wget \
        vim \
        nano \
        mysql-client \
        php-xdebug \
    && apt-get clean

#####################################
# subversion
#####################################
RUN apt-get update
RUN wget http://opensource.wandisco.com/1.11/scripts/subversion_installer_1.11.sh
RUN chmod +x subversion_installer_1.11.sh
RUN /bin/sh subversion_installer_1.11.sh

#####################################
# mysql
#####################################
# Import MySQL 5.7 Key
# gpg: key 5072E1F5: public key "MySQL Release Engineering <mysql-build@oss.oracle.com>" imported
RUN apt-get update
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 5072E1F5
RUN echo "deb http://repo.mysql.com/apt/ubuntu/ trusty mysql-5.7" | tee -a /etc/apt/sources.list.d/mysql.list
RUN echo "mysql-community-server mysql-community-server/data-dir select ''" | debconf-set-selections;\
    echo "mysql-community-server mysql-community-server/root-pass password $MYSQL_PASS" | debconf-set-selections;\
    echo "mysql-community-server mysql-community-server/re-root-pass password $MYSQL_PASS" | debconf-set-selections;\
    apt-get install -y mysql-server mysql-client libmysqlclient-dev

#####################################
# Composer:
#####################################

# Install composer and add its bin to the PATH.
RUN curl -s http://getcomposer.org/installer | php && \
    echo "export PATH=${PATH}:/var/www/vendor/bin" >> ~/.bashrc && \
    mv composer.phar /usr/local/bin/composer

#####################################
# npm, nvm & yarn:
#####################################
RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash 
RUN . ~/.bashrc

RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN npm install -g yarn

RUN node -v
RUN npm -v
RUN yarn -v

#####################################
# wp-cli:
#####################################
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp && \
    wp --info
# Source the bash
RUN . ~/.bashrc