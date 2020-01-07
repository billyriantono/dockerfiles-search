FROM webdevops/base:ubuntu-15.04

MAINTAINER Eduardo Pinuaga <info@did-web.com>

ADD . /var/www/html
RUN apt-get update && \
    apt-get  install -y vim



# Install php
RUN /usr/local/bin/apt-install \
        php5-cli \
        php5-fpm \
        php5-json \
        php5-intl \
        php5-curl \
        php5-mysqlnd \
        php5-xdebug \
        php5-memcached \
        php5-mcrypt \
        php5-gd \
        php5-sqlite \
        php5-xmlrpc \
        php5-xsl \
        php5-geoip \
        php5-ldap \
        php5-memcache \
        php5-memcached \
        php5-imagick \
        php-pear \
    && pear channel-update pear.php.net \
    && pear upgrade-all \
    && pear config-set auto_discover 1 \
    && ln -sf /etc/php5/mods-available/mcrypt.in /etc/php5/cli/conf.d/20-mcrypt.ini \
    && ln -sf /etc/php5/mods-available/mcrypt.in /etc/php5/fpm/conf.d/20-mcrypt.ini \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer


EXPOSE 8000
