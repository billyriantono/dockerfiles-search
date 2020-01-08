ARG PHP_VERSION=7.3
# debian stretch-slim
FROM php:${PHP_VERSION}-cli-stretch

USER root
###########################################################################
# Add a non-root user to prevent files being created with root permissions on host machine.
###########################################################################
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

###########################################################################
# Set Timezone
###########################################################################

ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    groupadd -g ${PGID} www && \
    # useradd -u ${PUID} -g www -m www -G wheel && \
    useradd -u ${PUID} -g www -m www -s /bin/bash

# 切换阿里源
ARG CHANGE_SOURCE=false
RUN if [ ${CHANGE_SOURCE} = true ]; then \
#sed -i "1ideb http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
#deb-src http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
#deb http://mirrors.aliyun.com/debian-security stretch/updates main\n\
#deb-src http://mirrors.aliyun.com/debian-security stretch/updates main\n\
#deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
#deb-src http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
#deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n\
#deb-src http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n" /etc/apt/sources.list \
echo \
"deb http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb-src http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n" > /etc/apt/sources.list \
      && cat /etc/apt/sources.list \
;fi


#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",
#

# Install "curl", "libmemcached-dev", "libpq-dev", "libjpeg-dev",
#         "libpng-dev", "libfreetype6-dev", "libssl-dev", "libmcrypt-dev",

RUN set -xe && apt-get update -yqq \
  && apt-get install -y --no-install-recommends \
    curl \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    wget \
    vim \
    apt-utils \
    inetutils-ping \
    libzip-dev zip unzip \
    librdkafka-dev \
    git subversion mercurial bash patch make coreutils \
  && pecl channel-update pecl.php.net \
  && docker-php-ext-configure zip --with-libzip \
  # Install the zip extension
  &&  docker-php-ext-install zip

#####################################
# gd:
#####################################
# Install the PHP gd library
RUN docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
docker-php-ext-install gd \
# Install the PHP pdo_mysql extention
&& docker-php-ext-install pdo_mysql

###########################################################################
# pgsql
###########################################################################

ARG INSTALL_PGSQL=false

RUN if [ ${INSTALL_PGSQL} = true ]; then \
    # Install the pgsql extension
    docker-php-ext-install pgsql \
# Install the PHP pdo_pgsql extention
    && docker-php-ext-install pdo_pgsql \
;fi

###########################################################################
# pgsql client
###########################################################################

ARG INSTALL_PG_CLIENT=false

RUN if [ ${INSTALL_PG_CLIENT} = true ]; then \
# Create folders if not exists (https://github.com/tianon/docker-brew-debian/issues/65)
    mkdir -p /usr/share/man/man1 && \
    mkdir -p /usr/share/man/man7 && \
# Install the pgsql client
    apt-get install -y postgresql-client \
;fi

###########################################################################
# PHP REDIS EXTENSION
###########################################################################

ARG INSTALL_PHPREDIS=true

RUN if [ ${INSTALL_PHPREDIS} = true ]; then \
    # Install Php Redis Extension
    printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis \
;fi

###########################################################################
# MongoDB:
###########################################################################

ARG INSTALL_MONGO=false

RUN if [ ${INSTALL_MONGO} = true ]; then \
    # Install the mongodb extension
    if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then \
      pecl install mongo && \
      docker-php-ext-enable mongo \
    ;fi && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb \
;fi

###########################################################################
# AMQP:
###########################################################################

ARG INSTALL_AMQP=false

RUN if [ ${INSTALL_AMQP} = true ]; then \
    # download and install manually, to make sure it's compatible with ampq installed by pecl later
    # install cmake first
    apt-get update && apt-get -y install cmake && \
    curl -L -o /tmp/rabbitmq-c.tar.gz https://github.com/alanxz/rabbitmq-c/archive/master.tar.gz && \
    mkdir -p rabbitmq-c && \
    tar -C rabbitmq-c -zxvf /tmp/rabbitmq-c.tar.gz --strip 1 && \
    cd rabbitmq-c/ && \
    mkdir _build && cd _build/ && \
    cmake .. && \
    cmake --build . --target install && \
    # Install the amqp extension
    pecl install amqp && \
    docker-php-ext-enable amqp && \
    # Install the sockets extension
    docker-php-ext-install sockets \
;fi

############################################################################
## ZipArchive:
############################################################################
#
#ARG INSTALL_ZIP_ARCHIVE=false
#
#RUN if [ ${INSTALL_ZIP_ARCHIVE} = true ]; then \
#    # Install the zip extension
#    docker-php-ext-install zip \
#;fi

###########################################################################
# bcmath:
###########################################################################

ARG INSTALL_BCMATH=true

RUN if [ ${INSTALL_BCMATH} = true ]; then \
    # Install the bcmath extension
    docker-php-ext-install bcmath \
;fi

###########################################################################
# Exif:
###########################################################################

#ARG INSTALL_EXIF=false
#
#RUN if [ ${INSTALL_EXIF} = true ]; then \
#    # Enable Exif PHP extentions requirements
#    docker-php-ext-install exif \
#;fi

###########################################################################
# Opcache:
###########################################################################

ARG INSTALL_OPCACHE=true

RUN if [ ${INSTALL_OPCACHE} = true ]; then \
    docker-php-ext-install opcache \
;fi

# Copy opcache configration
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

###########################################################################
# Mysqli Modifications:
###########################################################################

ARG INSTALL_MYSQLI=false

RUN if [ ${INSTALL_MYSQLI} = true ]; then \
    docker-php-ext-install mysqli \
;fi

###########################################################################
# Tokenizer Modifications:
###########################################################################

ARG INSTALL_TOKENIZER=false

RUN if [ ${INSTALL_TOKENIZER} = true ]; then \
    docker-php-ext-install tokenizer \
;fi

###########################################################################
# Human Language and Character Encoding Support:
###########################################################################

ARG INSTALL_INTL=false

RUN if [ ${INSTALL_INTL} = true ]; then \
    # Install intl and requirements
    apt-get install -y zlib1g-dev libicu-dev g++ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl \
;fi

###########################################################################
# GHOSTSCRIPT: pdf转图片 配合 ImageMagick
###########################################################################

ARG INSTALL_GHOSTSCRIPT=false

RUN if [ ${INSTALL_GHOSTSCRIPT} = true ]; then \
    # Install the ghostscript extension
    # for PDF editing
    apt-get install -y \
    poppler-utils \
    ghostscript \
;fi

###########################################################################
# LDAP:
###########################################################################

ARG INSTALL_LDAP=false

RUN if [ ${INSTALL_LDAP} = true ]; then \
    apt-get install -y libldap2-dev && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap \
;fi

###########################################################################
# Image optimizers: 图片无损压缩
###########################################################################

ARG INSTALL_IMAGE_OPTIMIZERS=false

RUN if [ ${INSTALL_IMAGE_OPTIMIZERS} = true ]; then \
    apt-get install -y --force-yes jpegoptim optipng pngquant gifsicle \
;fi


###########################################################################
# ImageMagick:
###########################################################################

USER root

ARG INSTALL_IMAGEMAGICK=false

RUN if [ ${INSTALL_IMAGEMAGICK} = true ]; then \
    apt-get install -y libmagickwand-dev imagemagick && \
    pecl install imagick && \
    docker-php-ext-enable imagick \
;fi

###########################################################################
# IMAP:
###########################################################################

ARG INSTALL_IMAP=false

RUN if [ ${INSTALL_IMAP} = true ]; then \
    apt-get install -y libc-client-dev libkrb5-dev && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install imap \
;fi

###########################################################################
# Swoole EXTENSION
###########################################################################

ARG INSTALL_SWOOLE=true

RUN if [ ${INSTALL_SWOOLE} = true ]; then \
    # Install Php Swoole Extension
    if [ $(php -r "echo PHP_MAJOR_VERSION;") = "5" ]; then \
      pecl install swoole-2.0.10; \
    else \
      if [ $(php -r "echo PHP_MINOR_VERSION;") = "0" ]; then \
        pecl install swoole-2.2.0; \
      else \
        pecl install swoole; \
      fi \
    fi && \
    docker-php-ext-enable swoole \
    && pecl install inotify \
    && docker-php-ext-enable inotify \
    && php -m | grep -q 'swoole' \
;fi

###########################################################################
# rdkafka:
# https://arnaud-lb.github.io/php-rdkafka/phpdoc/rdkafka.installation.pecl.html
###########################################################################
ARG INSTALL_RDKAFKA=true
RUN if [ ${INSTALL_RDKAFKA} = true ]; then \
#        git clone https://github.com/edenhill/librdkafka.git && \
#        cd librdkafka && \
#        ./configure && \
#        make && make install && \
#        cd ../ && \
        pecl install rdkafka && \
        docker-php-ext-enable rdkafka \
;fi

###########################################################################
# yar:
# https://www.php.net/manual/zh/book.yar.php
###########################################################################
ARG INSTALL_YAR=false
RUN if [ ${INSTALL_YAR} = true ]; then \
        pecl install yar-2.0.5 && \
        docker-php-ext-enable yar \
;fi

###########################################################################
# Check PHP version:
###########################################################################

ARG PHP_VERSION=${PHP_VERSION}

RUN php -v | head -n 1 | grep -q "PHP ${PHP_VERSION}."

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

# 添加composer
ARG PHP_COMPOSER_VERSION=1.9.0
ADD https://getcomposer.org/download/${PHP_COMPOSER_VERSION}/composer.phar  /usr/local/bin/

#COPY ./composer.phar /usr/local/bin/composer.phar

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp

COPY ./laravel.ini /usr/local/etc/php/conf.d

RUN chmod +rx /usr/local/bin/composer.phar && \
    ln -s /usr/local/bin/composer.phar /usr/local/bin/composer && \
# Clean up
    apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
        rm /var/log/lastlog /var/log/faillog && \
        echo "fs.inotify.max_user_watches=1048576" >> /etc/sysctl.conf

WORKDIR /var/www/html
USER www
CMD ["php", "-m"]
VOLUME ["/var/www/html"]
EXPOSE 9000
