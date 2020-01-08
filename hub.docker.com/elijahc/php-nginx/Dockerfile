FROM nginx:stable

# Install php
RUN apt-get update && apt-get install -qy \
        curl \
        git \
        vim \
        openssh \
        php5-cli \
        php5-json \
        php5-curl \
        php5-mysqlnd \
        php5-xdebug \
        php5-sqlite \
        php-pear \
        && pear channel-update pear.php.net \
        && pear upgrade-all \
        && pear config-set auto_discover 1 \
        && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
