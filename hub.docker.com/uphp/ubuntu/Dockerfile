FROM ubuntu:14.04

LABEL maintainer exploitfate

# Install additional packages
RUN apt-get update
RUN apt-get install -y git curl rsync openssh-client zip unzip apt-transport-https

# Install php packages
RUN apt-get install -y php5-cli php5-curl php5-gd php5-imagick php5-intl php5-mcrypt  php5-memcache php5-memcached php5-mysql php5-pgsql php5-gearman php5-xcache php5-xmlrpc php5-gmp php5-mongo php5-redis

# Install composer and put binary into $PATH
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/ \
    && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

# Install composer asset plugin
RUN composer global require "fxp/composer-asset-plugin:^1.3.1"

# Install phpunit 4.8.*
RUN composer global require phpunit/phpunit ^4.8

# Install PHP Code sniffer 2.*
RUN composer global require squizlabs/php_codesniffer ^2

# Install PHP Xdebug package
RUN apt-get install -y php5-xdebug

# Delete all the apt list files since they're big and get stale quickly
RUN rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www/html

VOLUME /var/www/html

COPY php.sh /root/php.sh
RUN chmod 744 /root/php.sh
ENTRYPOINT ["/root/php.sh"]

CMD ["/bin/bash"]
