FROM maciver40/ubuntu-base

LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/config" ]

VOLUME [ "/var/www/html" ]

EXPOSE 80 443

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
ENV APACHE_SERVER_NAME websrv

RUN \
    apt-get update && \
    apt-get install -o DPkg::Options::="--force-confold" -y \
  	    apache2 \
        # Install php 7.2
        libapache2-mod-php7.2 \
        php7.2-cli \
        php7.2-json \
        php7.2-curl \
        php7.2-fpm \
        php7.2-gd \
        php7.2-ldap \
        php7.2-mbstring \
        php7.2-mysql \
        php7.2-soap \
        php7.2-sqlite3 \
        php7.2-xml \
        php7.2-zip \
        php7.2-intl \
        php-imagick \
        # Install tools
        openssl \
        graphicsmagick \
        imagemagick \
        ghostscript \
        mysql-client \
        iputils-ping \
        sqlite3 \
        ca-certificates && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
