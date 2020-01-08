FROM debian:jessie
MAINTAINER Benjamin Böhmke

# Install Latex
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install git curl doxygen \
        php5-adodb php5-cli php5-curl php5-dbg php5-exactimage php5-gd \
        php5-geoip php5-geos php5-gnupg php5-imagick php5-imap php5-intl \
        php5-json php5-lasso php5-ldap php5-librdf php5-libvirt-php \
        php5-mcrypt php5-memcache php5-memcached php5-mysql php5-oauth \
        php5-odbc php5-pgsql php5-readline php5-recode php5-redis php5-rrd \
        php5-sasl php5-sqlite php5-ssh2 php5-stomp php5-xdebug \
        php5-xmlrpc php5-xsl && \
    rm -rf /var/lib/apt/lists/*

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# set working directory
WORKDIR /data
VOLUME /data
