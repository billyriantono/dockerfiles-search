FROM tmenu/docker:apache2.2

MAINTAINER Thomas Menu <menu.tho@gmail.com>

RUN systemMods=" \
        php5 \
        libapache2-mod-php5 \
        php5-cli \
        php5-dev \
        php5-mongo \
        php5-curl \
        php5-xdebug \
        php5-imagick \
        php5-intl \
        php5-mysql \
        php5-gd \
        php-pear \
        php-apc \
    " \
    && apt-get update \
    && apt-get install -y $systemMods \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN a2enmod php5

COPY ./php/php.ini /etc/php5/apache2/

# Install php tools
RUN cd /var/www/html && \
    wget http://getcomposer.org/composer.phar && \
    chmod +x composer.phar && \
    mv composer.phar /usr/local/bin/composer && \
    wget http://get.sensiolabs.org/php-cs-fixer.phar && \
    chmod +x php-cs-fixer.phar && \
    mv php-cs-fixer.phar /usr/local/bin/php-cs-fixer

RUN echo "xdebug.max_nesting_level = 1000" >> /etc/php5/conf.d/20-xdebug.ini

CMD ["/run.sh"]