# Dockerfile for a ubuntu 12.04 image with stock php 5.4 with all extensions installed.

#
FROM debian:wheezy

# Set correct environment variables.
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No

# Our user in the container
USER root
WORKDIR /root

# Enable PHP 5.4 repo and update apt-get

run apt-get update

# Install and Test PHP
RUN apt-get install --no-install-recommends -y \
		curl ca-certificates \
		php5-cli \
		php5-dev \
		php5-xdebug \
		php-apc \
		php5-json \
		php5-memcached php5-memcache \
		php5-mysql \
		php5-sqlite php5-sybase php5-interbase php5-odbc \
		php5-mcrypt  \
		php5-gmp  \
		php5-intl \
		php5-geoip \
		php5-imagick php5-gd \
		php5-imap \
		php5-curl \
		php5-svn \
		php5-ps \
		php5-ming \
		php5-enchant \
		php5-xsl \
		php5-xmlrpc \
		php5-tidy \
		php5-recode \
		php5-fpm \
		#php5-readline \
		php5-pspell \
		php-pear && \
		php --version && \
		php -m


# Install stuff
RUN apt-get update \
  && apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    #libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxslt1-dev \
    git \
    vim \
    wget \
    lynx \
    psmisc \
    yui-compressor \
    jpegoptim \
    cron \
    supervisor \
    libmagickwand-dev \
    bzip2 \
    php5-gd \
    php5-intl \
    #php5-mbstring \
    php5-mcrypt \
    #php5-pdo_mysql \
    php5-xsl \
    zip \
    #php5-opcache \
    #php5-soap \
    php5-imagick \
  && apt-get clean


# Install Composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- \
      --install-dir=/usr/local/bin \
      --filename=composer \
      --version=1.1.2

# Install MageRun
RUN cd /usr/local/bin && \
    wget https://files.magerun.net/n98-magerun.phar && \
    chmod +x ./n98-magerun.phar

# Tidy up
RUN apt-get -y autoremove && apt-get clean && apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Allow mounting files
VOLUME ["/root"]

RUN sed -i 's/listen = \/var\/run\/php5-fpm.sock/listen = 9000/' /etc/php5/fpm/pool.d/www.conf

# PHP is our entry point
CMD ["/usr/bin/php"]
