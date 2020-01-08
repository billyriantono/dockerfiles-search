FROM php:7.1-cli
MAINTAINER Philip Johansson <philip.johansson@duva.se>
ENV DEBIAN_FRONTEND noninteractive

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    set -ex && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        gnupg \
        apt-transport-https \
        software-properties-common && \
    \
    ## Add repository for docker
    #add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    #curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    # Add repository for MySQL 8.0
    add-apt-repository "deb https://repo.mysql.com/apt/debian/ stretch mysql-8.0" && \
    curl -fsSL https://repo.mysql.com/RPM-GPG-KEY-mysql | apt-key add - && \
    # Add repository for yarn
    add-apt-repository "deb https://dl.yarnpkg.com/debian/ stable main" && \
    curl -fsSL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    \
    curl -fsSL https://deb.nodesource.com/setup_12.x | bash - && \
    \
    apt-get update && \
    apt-get install -y \
      git \
      libfreetype6-dev \
      libicu-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpng-dev \
      libsqlite3-dev \
      libxslt-dev \
      libssh2-1 \
      libssh2-1-dev \
      subversion \
      unzip \
      zip \
      zlib1g-dev \
      yarn \
      nodejs \
      mysql-community-client \
      #docker-ce \
      xvfb \
      libgtk2.0-0 \
      libnotify-dev \
      libgconf-2-4 \
      libnss3 \
      libxss1 \
      libasound2 \
      && \
    docker-php-ext-configure gd \
      --with-gd \
      --with-freetype-dir=/usr/include/ \
      --with-png-dir=/usr/include/ \
      --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j $NPROC pdo_mysql mysqli mcrypt gd exif intl xsl soap zip opcache && \
    pecl install -o -f redis && \
    pecl install xdebug-2.6.1 && \
    pecl install igbinary-2.0.8 && \
    pecl install apcu-5.1.16 && \
    pecl install ssh2-1.1.2 && \
    docker-php-ext-enable redis && \
    docker-php-ext-enable xdebug && \
    docker-php-ext-enable igbinary && \
    docker-php-ext-enable apcu && \
    docker-php-ext-enable ssh2 && \
    docker-php-source delete && \
    apt-get remove -y \
      gnupg \
      software-properties-common \
      && \
    apt-get autoremove -y && \
    apt-get clean

RUN set -ex && \
    curl -fsSL https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer diagnose

COPY wp-cli.phar /usr/local/bin/wp
RUN set -ex && \
    wp --info

COPY rootfs/* /
