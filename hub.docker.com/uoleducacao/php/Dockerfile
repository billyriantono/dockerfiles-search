FROM php:7.1.18-fpm

# Environment Variables
ENV TERM xterm
ENV EDITOR nano
ENV DEBIAN_FRONTEND noninteractive
ENV ACCEPT_EULA Y
ENV php_conf /usr/local/etc/php/php.ini
ENV fpm_conf /usr/local/etc/php-fpm.conf
ENV fpm_pool_conf /usr/local/etc/php-fpm.d/*.conf

# Install PHP extensions and PECL modules.
RUN buildDeps=" \
        libbz2-dev \
        libxslt-dev \
        libmemcached-dev \
        default-libmysqlclient-dev \
        libsasl2-dev \
    " \
    runtimeDeps=" \
        libpcre3 \
        openssh-client \
        nano \
        vim \
        nginx \
        curl \
        wget \
        git \
        cron \
        mlocate \
        gnupg2 \
        apt-transport-https \
        libfreetype6-dev \
        libicu-dev \
        libjpeg-dev \
        libldap2-dev \
        libmcrypt-dev \
        libmemcachedutil2 \
        libpng-dev \
        libpq-dev \
        libxml2-dev \
        libcurl4-openssl-dev \
        sqlite3 \
        libsqlite3-dev \
        autoconf \
        pkg-config \
        ca-certificates \
        tdsodbc \
        freetds-common \
        freetds-bin \
        python-pip \
    " \
    && apt-get update \
    && apt-get install -y --assume-yes apt-utils \
    && apt-get install -y $buildDeps $runtimeDeps \
    && docker-php-ext-install bcmath bz2 calendar ctype exif iconv intl json mbstring mcrypt mysqli opcache pdo_mysql pdo_pgsql pdo_sqlite pgsql soap xml xsl zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install exif \
    && pecl install memcached redis mongodb \
    && docker-php-ext-enable memcached.so redis.so mongodb.so

# Install Supervisor
RUN pip install --upgrade supervisor supervisor-stdout
ADD conf/supervisor/*.conf /etc/supervisor/

# Install sqlsrv and pdo_sqlsrv extensions
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN sqlsrvDeps=" \
        libgss3 \
        msodbcsql \
        mssql-tools \
        unixodbc-dev \
        locales \
    " \
    && apt-get -y update \
    && apt-get install -y $sqlsrvDeps \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen
RUN pecl install pdo_sqlsrv-4.3.0 sqlsrv-4.3.0 \
    && docker-php-ext-enable sqlsrv.so pdo_sqlsrv.so
ADD conf/sql/freetds.conf /etc/freetds/freetds.conf
ADD conf/sql/odbcinst.ini /etc/odbcinst.ini

# Install rdkafka
RUN cd /tmp \
 && wget https://github.com/edenhill/librdkafka/archive/v0.11.0.tar.gz \
 && tar -xzf v0.11.0.tar.gz \
 && cd /tmp/librdkafka-0.11.0 \
 && ./configure && make && make install \
 && cd ../ && rm -rf librdkafka-0.11.0 \
 && pecl install rdkafka \
 && docker-php-ext-enable rdkafka

# Create php.ini
ADD conf/webserver/php.ini ${php_conf}

# Tweak PHP-FPM config
RUN sed -i \
        -e "s/;daemonize\s*=\s*yes/daemonize = no/g" \
        ${fpm_conf} && \
    sed -i \
        -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" \
        -e "s/pm.max_children = 5/pm.max_children = 100/g" \
        -e "s/pm.start_servers = 2/pm.start_servers = 3/g" \
        -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 2/g" \
        -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 4/g" \
        -e "s/;pm.max_requests = 500/pm.max_requests = 200/g" \
        -e "s/;listen.owner = .*/listen.owner = www-data/g" \
        -e "s/;listen.group = .*/listen.group = www-data/g" \
        -e "s/;listen.mode = 0660/listen.mode = 0666/g" \
        -e "s/listen = .*/listen = \/var\/run\/php-fpm\/php-fpm.sock/g" \
        ${fpm_pool_conf} && \
    mkdir -p /var/run/php-fpm

# Config Nginx
RUN mkdir -p /etc/nginx
RUN mkdir -p /run/nginx
RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/webserver/nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /etc/nginx/sites-available/ && \
    mkdir -p /etc/nginx/sites-enabled/ && \
    rm -Rf /var/www/*
ADD conf/webserver/nginx-site.conf /etc/nginx/sites-available/default.conf
RUN rm -Rf /etc/nginx/sites-enabled/*
RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf

# Add bin folder of composer to PATH.
ENV PATH /var/www/html/vendor/bin:$PATH

# Install Composer
RUN curl --retry 5 --retry-delay 0 -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Config Cron
ADD conf/cron/crontab /etc/cron.d/workspace-cron
RUN chmod 0644 /etc/cron.d/workspace-cron

# Allow to include custom php-fpm config, e.g. to set environment variables
ADD scripts/env.php /usr/local/etc/
RUN echo 'include=/usr/local/etc/conf.d/*' >> /usr/local/etc/php-fpm.conf \
    && mkdir /usr/local/etc/conf.d/

# Source the bash
RUN . ~/.bashrc

# Clean up and update locate database
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get purge -y --auto-remove $buildDeps \
    && updatedb

EXPOSE 80

WORKDIR /var/www/html

# PHP-FPM Daemon
ADD scripts/init.d/php-fpm /etc/init.d/

# Startup Script
ADD scripts/start.sh /start.sh
RUN chmod 0700 /start.sh
CMD ["/bin/bash", "-c", "/start.sh"]

ENV DEBIAN_FRONTEND teletype