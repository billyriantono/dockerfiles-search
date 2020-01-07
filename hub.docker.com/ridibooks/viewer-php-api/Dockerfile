FROM ridibooks/php:7.1-base
MAINTAINER Seonkuk Kim <kering@ridi.com>

# Install packages
RUN apt-get update --fix-missing && apt-get install --no-install-recommends -y software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update --fix-missing && apt-get install --no-install-recommends -y \
    # Common
    git wget python python-dev psmisc netcat gettext-base unzip \
    # Apache
    apache2 libapache2-mod-php7.1 \
    # PHP
    php7.1-cli php7.1-curl php7.1-mbstring php7.1-mcrypt php7.1-mysql php7.1-apcu php7.1-memcache php7.1-zip php7.1-bcmath \
    # For PHP zip extension
    zlib1g-dev \
    # For Cassandra php-driver
    g++ make cmake libssl-dev libgmp-dev openssl libpcre3-dev

RUN wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.18.0/libuv_1.18.0-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.18.0/libuv-dev_1.18.0-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.8.1/cassandra-cpp-driver_2.8.1-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.8.1/cassandra-cpp-driver-dev_2.8.1-1_amd64.deb && \
    dpkg -i libuv_1.18.0-1_amd64.deb && \
    dpkg -i libuv-dev_1.18.0-1_amd64.deb && \
    dpkg -i cassandra-cpp-driver_2.8.1-1_amd64.deb && \
    dpkg -i cassandra-cpp-driver-dev_2.8.1-1_amd64.deb
    
RUN apt-get autoclean -y && apt-get clean -y

# PHP zip extension is required so Composer can use packages from dist
RUN docker-php-ext-install zip

# Install datastax php-driver for Cassandra
RUN pecl install cassandra
RUN echo "extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/cassandra.so" >> /etc/php/7.1/mods-available/cassandra.ini && \
    phpenmod cassandra 

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer
