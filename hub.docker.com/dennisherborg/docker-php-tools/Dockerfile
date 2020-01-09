FROM alpine
MAINTAINER Dennis Herborg <info@inspireart.de>

ENV DATE_TIMEZONE Europe/Berlin

RUN apk --update add \
    openssl \
    openssh-client \

    php7 \
    php7-iconv \
    php7-mcrypt \
    php7-gd \
    php7-bz2 \
    php7-calendar \
    php7-exif \
    php7-ftp \
    php7-gettext \
    php7-mysqli \
    php7-pdo_mysql \
    php7-sockets \
    php7-wddx \
    php7-xsl \
    php7-zip \
    php7-openssl \
    php7-json \
    php7-phar \
    php7-zlib \
    php7-mbstring \
    php7-xml \
    php7-bcmath \
    php7-pcntl \
    php7-xdebug \
    php7-pear \
    php7-ctype \
    php7-opcache \
    php7-soap \
    php7-intl \
    php7-ftp \
    php7-session \
    php7-posix \

    libssl1.0 \
    curl && \

    rm -f /var/cache/apk/* && \

    ln -s /usr/bin/php7 /usr/bin/php && \
    echo "date.timezone=${DATE_TIMEZONE}" > /etc/php7/conf.d/timezone.ini && \
    echo "memory_limit=-1" > /etc/php7/conf.d/memory-limit.ini && \
    echo "zend_extension=xdebug.so" > /etc/php7/conf.d/xdebug.ini

# Add global composer binary directory to PATH
ENV PATH /root/.composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Pass --no-interaction flag to every command
ENV COMPOSER_NO_INTERACTION 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer && \
    curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig && \
    php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" && \
    php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('/tmp/composer-setup.php');" && \
    php -r "unlink('/tmp/composer-setup.sig');" && \

# Install Composer packages
    composer self-update && \
    composer global require phpunit/phpunit && \
    composer global require phpmetrics/phpmetrics && \
    composer global require squizlabs/php_codesniffer && \
    composer global require phpmd/phpmd && \
    composer global require phploc/phploc && \
    composer global require sebastian/phpcpd && \
    composer global require pdepend/pdepend && \
    composer global require phing/phing && \
    composer global require friendsofphp/php-cs-fixer && \
    composer global require codegyre/robo && \
    composer global require behat/behat && \
    composer global update && \
    composer clear-cache

# Set up the volumes and working directory
VOLUME ["/app"]
WORKDIR /app

CMD ["php", "-a"]
