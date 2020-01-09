FROM php:7.2-apache

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
  && rm -rf /var/lib/apt/lists/*


 
  # Install the PHP pdo_mysql extention
  RUN docker-php-ext-install pdo_mysql \
  # Install the PHP pdo_pgsql extention
  && docker-php-ext-install pdo_pgsql \
  # Install the PHP gd library
  && docker-php-ext-configure gd \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd


# always run apt update when start and after add new source list, then clean up at end.
RUN apt-get update -yqq && \
    apt-get install -y apt-utils && \
    pecl channel-update pecl.php.net

###########################################################################
# SSH2:
###########################################################################

RUN apt-get -y install libssh2-1-dev && \
        pecl install -a ssh2-1.1.2 && \
    docker-php-ext-enable ssh2

###########################################################################
# libfaketime:
###########################################################################

RUN apt-get install -y libfaketime

###########################################################################
# SOAP:
###########################################################################

RUN rm /etc/apt/preferences.d/no-debian-php && \
    apt-get -y install libxml2-dev php-soap && \
    docker-php-ext-install soap

###########################################################################
# pgsql
###########################################################################


RUN docker-php-ext-install pgsql

###########################################################################
# pgsql client
###########################################################################

RUN mkdir -p /usr/share/man/man1 && \
    mkdir -p /usr/share/man/man7 && \
    # Install the pgsql client
    apt-get install -y postgresql-client 

###########################################################################
# xDebug:
###########################################################################

RUN pecl install xdebug && \
  docker-php-ext-enable xdebug

# Copy xdebug configuration for remote debugging
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN sed -i "s/xdebug.remote_autostart=0/xdebug.remote_autostart=1/" /usr/local/etc/php/conf.d/xdebug.ini && \
    sed -i "s/xdebug.remote_enable=0/xdebug.remote_enable=1/" /usr/local/etc/php/conf.d/xdebug.ini && \
    sed -i "s/xdebug.cli_color=0/xdebug.cli_color=1/" /usr/local/etc/php/conf.d/xdebug.ini

###########################################################################
# Phpdbg:
###########################################################################


#RUN apt-get install -y --force-yes php7.2-phpdbg

###########################################################################
# PHP REDIS EXTENSION
###########################################################################


RUN printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

###########################################################################
# MongoDB:
###########################################################################


RUN pecl install mongodb && \
    docker-php-ext-enable mongodb

###########################################################################
# AMQP:
###########################################################################

RUN apt-get install librabbitmq-dev -y && \
    # Install the amqp extension
    pecl install amqp && \
    docker-php-ext-enable amqp

###########################################################################
# ZipArchive:
###########################################################################

RUN apt-get install libzip-dev libbz2-dev -y && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip

###########################################################################
# pcntl
###########################################################################

RUN docker-php-ext-install pcntl bz2

###########################################################################
# bcmath:
###########################################################################


RUN docker-php-ext-install bcmath

###########################################################################
# GMP (GNU Multiple Precision):
###########################################################################

RUN  apt-get install -y libgmp-dev && \
    ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
    docker-php-ext-install gmp 

###########################################################################
# PHP Memcached:
###########################################################################


RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
    && mkdir -p memcached \
    && tar -C memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
    && ( \
        cd memcached \
        && phpize \
        && ./configure \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r memcached \
    && rm /tmp/memcached.tar.gz \
    && docker-php-ext-enable memcached

###########################################################################
# Exif:
###########################################################################

RUN docker-php-ext-install exif

###########################################################################
# IonCube Loader:
###########################################################################



RUN curl -L -o /tmp/ioncube_loaders_lin_x86-64.tar.gz https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && tar zxpf /tmp/ioncube_loaders_lin_x86-64.tar.gz -C /tmp \
    && mv /tmp/ioncube/ioncube_loader_lin_7.2.so $(php -r "echo ini_get('extension_dir');")/ioncube_loader.so \
    && printf "zend_extension=ioncube_loader.so\n" > $PHP_INI_DIR/conf.d/0ioncube.ini \
    && rm -rf /tmp/ioncube* 

###########################################################################
# Opcache:
###########################################################################

RUN docker-php-ext-install opcache 
# Copy opcache configration
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

###########################################################################
# Mysqli Modifications:
###########################################################################

RUN docker-php-ext-install mysqli
###########################################################################
# Human Language and Character Encoding Support:
###########################################################################


RUN apt-get install -y zlib1g-dev libicu-dev g++ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl

###########################################################################
# GHOSTSCRIPT:
###########################################################################

ARG INSTALL_GHOSTSCRIPT=false

RUN apt-get install -y \
    poppler-utils \
    ghostscript 

###########################################################################
# LDAP:
###########################################################################


RUN apt-get install -y libldap2-dev && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap 

###########################################################################
# Image optimizers:
###########################################################################

RUN apt-get install -y jpegoptim optipng pngquant gifsicle

###########################################################################
# ImageMagick:
###########################################################################

RUN apt-get install -y libmagickwand-dev imagemagick && \
    pecl install imagick && \
    docker-php-ext-enable imagick

###########################################################################
# IMAP:
###########################################################################

RUN apt-get install -y libc-client-dev libkrb5-dev && \
    rm -r /var/lib/apt/lists/* && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install imap

###########################################################################
# Calendar:
###########################################################################


RUN docker-php-ext-configure calendar && \
    docker-php-ext-install calendar



#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

COPY ./laravel.ini /usr/local/etc/php/conf.d
COPY ./xlaravel.pool.conf /usr/local/etc/php-fpm.d/


# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 www-data

# Adding the faketime library to the preload file needs to be done last
# otherwise it will preload it for all commands that follow in this file
RUN echo "/usr/lib/x86_64-linux-gnu/faketime/libfaketime.so.1" > /etc/ld.so.preload 

WORKDIR /var/www/html

RUN apt-get update
RUN apt-get install -y \
   git \
   vim \
   cron \
   zip \
   unzip \
   nano \
   libmemcached-dev \
   curl \
   mariadb-client \
   sendmail-bin \
   sendmail \
   wget \
   sudo \
   bash-completion

RUN curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
RUN curl -o ~/.git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh

# Install composer
RUN wget https://getcomposer.org/download/1.7.2/composer.phar && chmod +x composer.phar && \
   mv composer.phar /usr/local/bin/composer && \
   # Install PHPUnit
  curl -sSL https://phar.phpunit.de/phpunit.phar -o phpunit.phar && \
    chmod +x phpunit.phar && \
       mv phpunit.phar /usr/local/bin/phpunit && \

 # Install Drupal Console
   curl https://drupalconsole.com/installer -o /usr/local/bin/drupal && \
   chmod +x /usr/local/bin/drupal && \
    echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> /root/.bashrc &&\
    echo 'source /root/bash_alias'

RUN composer global require drush/drush:8.* && \
    composer global require "hirak/prestissimo:^0.3"
##Platform
RUN cd ~ && curl -sS https://platform.sh/cli/installer | php && curl -O https://raw.githubusercontent.com/pantheon-systems/terminus-installer/master/builds/installer.phar && php installer.phar install
COPY bash_alias /root/.bash_alias
COPY php71.ini   /usr/local/etc/php/conf.d/php.ini
RUN echo "export TERM=xterm"  >> ~/.bashrc
RUN echo "source /root/.bash_alias"  >> ~/.bashrc

RUN { \
    echo 'opcache.memory_consumption=128'; \
    echo 'opcache.interned_strings_buffer=8'; \
    echo 'opcache.max_accelerated_files=4000'; \
    echo 'opcache.revalidate_freq=5'; \
    echo 'opcache.fast_shutdown=1'; \
    echo 'opcache.enable_cli=1'; \
  } > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN a2enmod vhost_alias ssl