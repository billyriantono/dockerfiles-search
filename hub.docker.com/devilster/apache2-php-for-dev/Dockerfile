FROM  phusion/baseimage

LABEL maintainer="Devil.Ster.1"
LABEL version="1.0.1"

ARG PHP_VER=7.1

ENV DEBIAN_FRONTEND noninteractive

# START Locales Install
RUN apt-get update && apt-get install -y --no-install-recommends \
        locales && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LANG=en_US.UTF-8
# END Locales Install

ENV TERM xterm

# START Install Apache2
ENV APACHE_RUN_USER     www-data
ENV APACHE_RUN_GROUP    www-data
ENV WEB_DOCUMENT_ROOT   /var/www/
ENV APACHE_LOG_DIR      /var/log/apache2

RUN apt-get update && apt-get install -y --no-install-recommends \
    --allow-downgrades --allow-remove-essential --allow-change-held-packages \
        apache2 \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# END Install Apache2

# START Configure Apache2
RUN a2enmod rewrite
RUN a2enmod ssl

RUN mkdir /etc/apache2/ssl
COPY certs /etc/apache2/ssl

COPY default-sites /etc/apache2/sites-available
RUN a2ensite default-ssl

# Autostart
RUN mkdir /etc/service/apache
ADD apache_start.sh /etc/service/apache/run
RUN chmod +x /etc/service/apache/run
# END Configure Apache2

# START Install Additional Soft
RUN apt-get update && apt-get install -y --no-install-recommends \
    --allow-downgrades --allow-remove-essential --allow-change-held-packages \
        wget \
        mcrypt \
        curl \
        gcc \
        cmake \
        make \
        postgresql-client \
        unzip \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# END Install Additional Soft

# START PHP INSTALL
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository -y ppa:ondrej/php

RUN apt-get update && apt-get install -y --no-install-recommends \
        --allow-downgrades --allow-remove-essential --allow-change-held-packages \
        libapache2-mod-php$PHP_VER \
        php$PHP_VER \
        php$PHP_VER-common \
        php$PHP_VER-cli \
        php$PHP_VER-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# END PHP INSTALL

# START PHP Modules Install
RUN apt-get update && apt-get install -y --no-install-recommends \
        --allow-downgrades --allow-remove-essential --allow-change-held-packages \
        php$PHP_VER-curl \
        php$PHP_VER-xmlrpc \
        php$PHP_VER-pspell \
        php$PHP_VER-gd \
        php$PHP_VER-pdo \
        php$PHP_VER-mbstring \
        php$PHP_VER-soap  \
        php$PHP_VER-xml \
        php$PHP_VER-zip \
        php$PHP_VER-bcmath \
        php$PHP_VER-bz2 \
        php$PHP_VER-calendar \
        php$PHP_VER-opcache \
        php$PHP_VER-gettext \
        php$PHP_VER-iconv \
        php$PHP_VER-ldap \
        php$PHP_VER-odbc \
        php$PHP_VER-pgsql \
        php$PHP_VER-memcached  \
        php-pear \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN if [ "$PHP_VER" = "7.2" ] || [ "$PHP_VER" = "7.3" ]; \
        then echo "7.2 AND 7.3 DOES NOT SUPPORT PHP_MCRYPT"; \
        else \
            apt-get update && \
            apt-get install -y --no-install-recommends php$PHP_VER-mcrypt \
            && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*;  \
    fi
# END PHP Modules Install

# START Composer Install
RUN rm -f /usr/local/bin/composer
RUN php -r "copy('https://getcomposer.org/installer', '/composer-setup.php');"
RUN php /composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN php -r "unlink('/composer-setup.php');"
# END Composer Install

# START PHP Configuration
RUN sed -e 's/display_errors = Off/display_errors = On/' -i /etc/php/${PHP_VER}/apache2/php.ini
RUN sed -e 's/display_startup_errors = Off/display_startup_errors = On/' -i /etc/php/${PHP_VER}/apache2/php.ini
RUN sed -e 's/;error_log = php_errors.log/error_log = \/var\/log\/apache2\/php_error.log/' -i /etc/php/${PHP_VER}/apache2/php.ini

RUN sed -e 's/display_errors = Off/display_errors = On/' -i /etc/php/${PHP_VER}/cli/php.ini
RUN sed -e 's/display_startup_errors = Off/display_startup_errors = On/' -i /etc/php/${PHP_VER}/cli/php.ini
RUN sed -e 's/;error_log = php_errors.log/error_log = \/var\/log\/apache2\/php_error_cli.log/' -i /etc/php/${PHP_VER}/cli/php.ini
# END PHP Configuration


# START Install Redis Support For PHP
RUN mkdir /tmp/phpredis && \
    cd /tmp/phpredis/ && \
    wget https://github.com/phpredis/phpredis/archive/4.2.0.zip -O phpredis.zip && \
    unzip -o ./phpredis.zip && \
    mv ./phpredis-* ./phpredis && \
    cd ./phpredis && \
    phpize && \
    ./configure && \
    make && \
    make install && \
    echo "extension=redis.so" > /etc/php/${PHP_VER}/mods-available/redis.ini && \
    ln -s /etc/php/${PHP_VER}/mods-available/redis.ini /etc/php/${PHP_VER}/apache2/conf.d/redis.ini && \
    ln -s /etc/php/${PHP_VER}/mods-available/redis.ini /etc/php/${PHP_VER}/cli/conf.d/redis.ini && \
    rm -fr /tmp/phpredis
# END Install Redis Support For PHP

# START Install XDebug Support
RUN pecl channel-update pecl.php.net && \
    pecl install xdebug && \
    echo "zend_extension=xdebug.so" > /etc/php/${PHP_VER}/mods-available/xdebug.ini && \
    ln -s /etc/php/${PHP_VER}/mods-available/xdebug.ini /etc/php/${PHP_VER}/apache2/conf.d/xdebug.ini && \
    ln -s /etc/php/${PHP_VER}/mods-available/xdebug.ini /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini

RUN echo "xdebug.remote_enable=1" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back = 0" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.remote_mode=req" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini \
    && echo "xdebug.idekey=\"PHPSTORM\"" >> /etc/php/${PHP_VER}/cli/conf.d/xdebug.ini

# END Install XDebug Support

WORKDIR /var/www

# For Linux - write permissions for volumes
RUN usermod -u 1000 www-data

EXPOSE 80
EXPOSE 443