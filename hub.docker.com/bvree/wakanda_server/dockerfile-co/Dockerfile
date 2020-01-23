FROM phpdockerio/php56-fpm:latest
MAINTAINER eu@brunolima.me
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php5-mongo php5-mysql php5-pgsql php5-redis php5-sqlite php5-adodb php5-enchant php5-exactimage php5-gd php5-gearman php5-geos php5-gmp php5-geoip php5-gnupg php5-pecl-http php5-igbinary php5-imap php5-imagick php5-ldap php5-libvirt-php php5-radius php5-pspell php5-ssh2 php5-twig php5-xdebug php5-xmlrpc php5-xsl \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*