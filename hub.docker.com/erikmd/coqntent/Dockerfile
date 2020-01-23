FROM ericmugerwa/ubuntu:17.04

USER root

# Apache 2.4
RUN apt-get update; \
    apt-get -y install \
        apache2; \
    rm -rf /var/log/apache2/*; \
    rm -rf /var/log/php/*; \
    rm -rf /var/www/*; \
    # apache config
    a2dissite 000-default; \
    a2enmod rewrite; \
    a2enmod headers; \
    a2enmod status

# Set PHP environment
ENV PHP_APACHE_INI             /etc/php/7.1/apache2/php.ini
ENV PHP_CLI_INI                /etc/php/7.1/cli/php.ini  
ENV PHP_APACHE_APP_INI         /etc/php/7.0/apache2/conf.d/10-app.ini
ENV PHP_CLI_APP_INI            /etc/php/7.0/cli/conf.d/10-app.ini
ENV PHP_MODS_AVAILABLE_DIR     /etc/php/7.1/mods-available
ENV PHP_ERROR_LOG              ${LOG_DIR}/php.log
ENV XDEBUG_LOG                 ${LOG_DIR}/xdebug.log

# Php log directories
RUN touch ${PHP_ERROR_LOG}; \
    chown ${APACHE_USER}:${APACHE_GROUP} ${PHP_ERROR_LOG}; \
    chmod 600 ${PHP_ERROR_LOG}; \
    touch ${XDEBUG_LOG}; \
    chown ${APACHE_USER}:${APACHE_GROUP} ${XDEBUG_LOG}; \
    chmod 600 ${XDEBUG_LOG}

# Install PHP 7.1 (core)
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php; \
    apt-get update; \
    apt-get -y install \
        php7.1 \
        php7.1-dev \
        php7.1-cli \
        php7.1-mysql \
        php7.1-sqlite3 \
        php7.1-mcrypt \
        php7.1-curl \
        php7.1-soap \
        php7.1-gd \
        php7.1-dom \
        php7.1-mbstring \
        php7.1-zip \
        php7.1-xml \
        php7.1-intl \
        php7.1-tidy \
        php7.1-gmp \
        libapache2-mod-php7.1

# PHP 7.1 (additional extensions)
RUN apt-get -y install \
        php-memcache \
        php-redis \
        php7.1-xdebug \
        imagemagick \
        php-imagick \
        librabbitmq4 \
        php-amqp \
        php-uuid \
        php-igbinary

# Install Pecl extensions
RUN apt-get -y install \
        php-pear; \
    pear config-set php_ini ${PHP_APACHE_INI}; \
    pecl config-set php_ini ${PHP_APACHE_INI}; \
    pecl install libsodium

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# PHP QA tools
USER ${ADMIN_USER}
RUN composer global require phpunit/phpunit ^6.1; \
    composer global require phpunit/dbunit ^3.0; \
    composer global require phpspec/phpspec ^3.3; \
    composer global require phing/phing ^2.16; \
    # composer global require phpdocumentor/phpdocumentor; \ [incompatible]
    composer global require sebastian/phpcpd ^3.0; \
    composer global require phploc/phploc ^3.0; \
    composer global require phpmd/phpmd ^2.6; \
    composer global require squizlabs/php_codesniffer ^2.8; \
    composer global update --optimize-autoloader

# Configure the executable
EXPOSE 80
EXPOSE 443
LABEL name="Ubuntu/PHP-7.1-Apache-2.4" description="PHP 7.1 + Apache 2.4"
