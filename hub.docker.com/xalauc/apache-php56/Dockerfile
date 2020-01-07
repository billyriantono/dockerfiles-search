FROM ubuntu:14.04.4
MAINTAINER Ben Blanks <ben@d15k.com>

# Set the timezone to Australia/Sydney
RUN ln -sf /usr/share/zoneinfo/Australia/Sydney /etc/localtime

##
# Install the packages
#
RUN apt-get update --no-install-recommends -y && \
    apt-get install --no-install-recommends -y software-properties-common language-pack-en-base &&\
    locale-gen en_US.UTF-8 &&\
    LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php --yes &&\
    apt-get update --no-install-recommends -y

RUN apt-get install --no-install-recommends -y \
    vim \
    wget \
    apache2 \
    php5.6 \
    php5.6-cli \
    php5.6-curl \
    php5.6-dev \
    php5.6-gd \
    php5.6-sqlite \
    php5.6-mysql \
    php5.6-opcache \
    php5.6-mcrypt \
    php5.6-mbstring \
    php5.6-json \
    php5.6-intl \
    php5.6-xml \
    php5.6-xsl \
    php5.6-zip \
    sendmail \
    openssl \
    make \
    ca-certificates \
    curl \
    wget \
    git \
    openssh-client

##
# Clean the apt-get repo cache.
#
RUN apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

##
# Remove the html directory so we have a clean www directory.
#
RUN rm -rf /var/www/html &&\
    rm /etc/apache2/sites-enabled/000-default.conf &&\
    rm /etc/apache2/conf-enabled/other-vhosts-access-log.conf

##
# Install the developer toolchain
#
RUN wget https://phar.phpunit.de/phpunit.phar &&\
    chmod a+x phpunit.phar &&\
    mv phpunit.phar /usr/local/bin/phpunit

##
# Installing wp-cli for use with wordpress projects.
#
RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar &&\
    chmod +x wp-cli.phar &&\
    mv wp-cli.phar /usr/local/bin/wp

##
# Installing composer.
#
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

##
# Reconfigure PHP
#
RUN sed -i 's/display_errors = Off/display_errors = On/g' /etc/php/5.6/apache2/php.ini &&\
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 102M/g' /etc/php/5.6/apache2/php.ini &&\
    sed -i 's/post_max_size = 8M/post_max_size = 108M/g' /etc/php/5.6/apache2/php.ini &&\
    sed -i 's/;date.timezone =/date.timezone = "Australia\/Sydney"/g' /etc/php/5.6/apache2/php.ini &&\
    sed -i 's/;error_log = syslog/error_log = syslog/g' /etc/php/5.6/apache2/php.ini &&\
    phpenmod mcrypt

##
# Install XDebug into PHP
#
RUN wget http://xdebug.org/files/xdebug-2.4.0.tgz && tar -xvzf xdebug-2.4.0.tgz && cd xdebug-2.4.0 && phpize && ./configure && make && cp modules/xdebug.so /usr/lib/php/20131226
RUN echo "[xdebug]" | tee -a /etc/php/5.6/apache2/conf.d/20-xdebug.ini > /dev/null &&\
    echo "zend_extension = /usr/lib/php/20131226/xdebug.so" | tee -a /etc/php/5.6/apache2/conf.d/20-xdebug.ini > /dev/null &&\
    echo "xdebug.profiler_enable_trigger = 1" | tee -a /etc/php/5.6/apache2/conf.d/20-xdebug.ini > /dev/null &&\
    echo "xdebug.profiler_output_dir = \"/var/www/profiler\"" | tee -a /etc/php/5.6/apache2/conf.d/20-xdebug.ini > /dev/null &&\
    rm -rf /xdebug-2.4.0

##
# Configure Apache
#
RUN a2enmod headers rewrite ssl

##
# Create the WWW user.
#
RUN useradd www &&\
    mkdir -p /home/www &&\
    chown www:www /home/www &&\
    chmod 0700 /home/www &&\
    chown www:www-data /var/www

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint
RUN chmod 0755 /usr/local/bin/docker-entrypoint &&\
    mkdir /docker-tools &&\
    ln -s /usr/local/bin/docker-entrypoint /

VOLUME /var/www/
VOLUME /etc/apache2/sites-enabled/

EXPOSE 80 443
ENTRYPOINT ["docker-entrypoint"]
