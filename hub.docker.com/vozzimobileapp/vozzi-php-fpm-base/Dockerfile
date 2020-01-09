FROM php:7.2-fpm

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    zip unzip \
    curl \
    git \
    ssh \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    vim \
    nano \
    libssl-dev && \
    rm -rf /var/lib/apt/lists/*

###########################################################################
# Base extensions
###########################################################################

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql

# always run apt update when start and after add new source list, then clean up at end.
RUN apt-get update -yqq && \
    apt-get install -y apt-utils && \
    pecl channel-update pecl.php.net

###########################################################################
# ssh2
###########################################################################

RUN apt-get -y install libssh2-1-dev && \
    pecl install -a ssh2-1.1.2; \
    docker-php-ext-enable ssh2

###########################################################################
# tokenizer
###########################################################################

RUN docker-php-ext-install tokenizer

###########################################################################
# ZipArchive:
###########################################################################

RUN apt-get install libzip-dev -y && \
   docker-php-ext-configure zip --with-libzip && \
   # Install the zip extension
   docker-php-ext-install zip

###########################################################################
# bcmath:
###########################################################################

RUN docker-php-ext-install bcmath

###########################################################################
# composer
###########################################################################

RUN curl --silent --show-error https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

###########################################################################
# Node
###########################################################################
RUN apt-get update && apt-get install -my wget gnupg
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

###########################################################################
# PHP gd library
###########################################################################

RUN docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd