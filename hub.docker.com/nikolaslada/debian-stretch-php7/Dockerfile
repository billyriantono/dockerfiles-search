FROM nikolaslada/debian-stretch

MAINTAINER Nikolas Lada <nikolas.lada@gmail.com>

ENV PHP_MODS_DIR=/etc/php/7.0/mods-available
ENV PHP_CLI_DIR=/etc/php/7.0/cli/
ENV PHP_CLI_CONF_DIR=${PHP_CLI_DIR}/conf.d
ENV TZ=Europe/Prague

RUN apt update && apt dist-upgrade -y && \
    apt install -y wget curl apt-transport-https ca-certificates && \
    apt update && \
    apt install -y --no-install-recommends \
        php-apcu \
        php-bcmath \
        php-bz2 \
        php-cli \
        php-curl \
        php-fpm \
        php-gd \
        php-geoip \
        php-gettext \
        php-imap \
	      php-imagick \
	      php-intl \
	      php-json \
        php-mbstring \
        php-mcrypt \
        php-mysql \
        php-pgsql \
        php-readline \
        php-redis \
        php-soap \
        php-sqlite3 \
        php-ssh2 \
        php-xdebug \
        php-xmlrpc \
        php-zip && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer global require "hirak/prestissimo:^0.3" && \
    ln -s ${PHP_MODS_DIR}/custom.ini ${PHP_CLI_CONF_DIR}/999-custom.ini && \
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get remove -y wget curl && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /var/lib/log/* /tmp/* /var/tmp/*

ADD conf.d/custom.ini ${PHP_MODS_DIR}/custom.ini

WORKDIR /srv

CMD ["php"]
