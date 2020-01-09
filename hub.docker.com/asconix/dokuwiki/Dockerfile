FROM debian:jessie

MAINTAINER Christoph Pilka <c.pilka@asconix.com>

# Version of DokuWiki to install
ENV DOKUWIKI_VERSION 2014-09-29b
ENV DOKUWIKI_MD5_CHECKSUM 605b14aad2f85f2f6a66ccb7c0a494e9

# Disable dialogs during package installation (no tty)
ENV DEBIAN_FRONTEND noninteractive

# Update APT repository and install dependencies
RUN apt-get update -q && \
    apt-get -y upgrade && \
    apt-get install -y \
    wget \
    locales \
    ntp \
    nginx \
    php5-fpm \
    php5-cli \
    supervisor

# Download, check and deploy DokuWiki
RUN wget -O /dokuwiki.tgz \
    "http://download.dokuwiki.org/src/dokuwiki/dokuwiki-$DOKUWIKI_VERSION.tgz"
RUN if [ "$DOKUWIKI_MD5_CHECKSUM" != "$(md5sum /dokuwiki.tgz | awk '{print($1)}')" ]; \
    then echo "The downloaded file is corrupt (wrong MD5 checksum)!"; exit 1; fi;
RUN tar -xzf dokuwiki.tgz
RUN mv "/dokuwiki-$DOKUWIKI_VERSION" /dokuwiki

# Set up ownership
RUN chown -R www-data:www-data /dokuwiki

# Remove downloaded archive file
RUN rm dokuwiki.tgz

# Locale
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Reconfigure locales
ADD ./etc/locale.gen /etc/locale.gen
RUN locale-gen && \
    dpkg-reconfigure locales && \
    update-locale LANG=en_US.UTF-8

# Nginx configuration
ADD ./etc/nginx/nginx.conf /etc/nginx/nginx.conf

# Nginx default site configuration
ADD ./etc/nginx/sites-available/default /etc/nginx/sites-available/default

# PHP-FPM configuration
ADD ./etc/php5/fpm/php-fpm.conf /etc/php5/fpm/php-fpm.conf

# Supervisor configuration
ADD ./etc/supervisor/conf.d/supervisor.conf /etc/supervisor/conf.d/supervisor.conf

# TODO
VOLUME ["/dokuwiki/", "/var/log/", "/run/"]

# Default command
CMD "/usr/bin/supervisord"
