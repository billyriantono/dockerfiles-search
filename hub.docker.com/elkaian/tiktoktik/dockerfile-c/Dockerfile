FROM elijahc/base:latest

# Install php
RUN apt-get update && apt-get install -qy \
        php5-cli \
        php5-json \
        php5-intl \
        php5-curl \
        php5-mysqlnd \
        php5-xdebug \
        php5-memcached \
        php5-gd \
        php5-sqlite \
        php5-xmlrpc \
        php5-xsl \
        php5-ldap \
        php-pear \
        && pear channel-update pear.php.net \
        && pear upgrade-all \
        && pear config-set auto_discover 1 \
        && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
