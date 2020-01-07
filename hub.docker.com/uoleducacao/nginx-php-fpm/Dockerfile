FROM phusion/baseimage:latest

RUN ACCEPT_EULA=Y
RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

ENV php_conf /etc/php/7.0/cli/php.ini
ENV fpm_conf /etc/php/7.0/fpm/pool.d/www.conf


# Install "software-properties-common" (for the "add-apt-repository")
RUN apt-get update && apt-get install -y \
    software-properties-common

# Add the "PHP 7" ppa
RUN add-apt-repository -y \
    ppa:ondrej/php

# Install PHP-CLI 7, some PHP extentions and some useful Tools with APT
RUN apt-get update && apt-get install -y \
        libpcre3 \
        openssh-client \
        nginx \
        curl \
        wget \
        git \
        nano \
        dialog \
        php7.0-bcmath \
        php7.0-cli \
        php7.0-common \
        php7.0-memcached \
        php7.0-fpm \
        php7.0-mysql \
        php7.0-pgsql \
        php7.0-sqlite \
        php7.0-sqlite3 \
        php7.0-sybase \
        php7.0-mcrypt \
        php7.0-mbstring \
        php7.0-ctype \
        php7.0-zip \
        php7.0-gd \
        php7.0-exif \
        php7.0-intl \
        php7.0-xml \
        php7.0-xsl \
        php7.0-curl \
        php7.0-json \
        php7.0-iconv \
        php7.0-soap \
        php-dev \
        php-xml \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libsslcommon2-dev \
        libxml2-dev \
        xz-utils \
        sqlite3 \
        libsqlite3-dev \
        autoconf \
        pkg-config \
        ca-certificates \
        freetds-common \
        freetds-bin \
        unixodbc

RUN apt-get install -y python-pip

# Config Sql Server ODBC
ADD conf/freetds.conf /etc/freetds/freetds.conf
ADD conf/odbcinst.ini /etc/odbcinst.ini

# Install mongodb extension
RUN pecl install mongodb
RUN echo "extension=mongodb.so" >> /etc/php/7.0/fpm/conf.d/mongodb.ini

#nginx
RUN mkdir -p /etc/nginx
RUN mkdir -p /var/www/app
RUN mkdir -p /run/nginx

# Copy our nginx config
RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/nginx.conf /etc/nginx/nginx.conf

# nginx site conf
RUN mkdir -p /etc/nginx/sites-available/ && \
mkdir -p /etc/nginx/sites-enabled/ && \
rm -Rf /var/www/* && \
mkdir /var/www/html/
ADD conf/nginx-site.conf /etc/nginx/sites-available/default.conf
RUN rm -Rf /etc/nginx/sites-enabled/*
RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf

# tweak php-fpm config
RUN sed -i \
        -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" \
        -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" \
        -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" \
        -e "s/variables_order = \"GPCS\"/variables_order = \"EGPCS\"/g" \
        ${php_conf} && \
    sed -i \
        -e "s/;daemonize\s*=\s*yes/daemonize = no/g" \
        -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" \
        -e "s/pm.max_children = 4/pm.max_children = 4/g" \
        -e "s/pm.start_servers = 2/pm.start_servers = 3/g" \
        -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 2/g" \
        -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 4/g" \
        -e "s/pm.max_requests = 500/pm.max_requests = 200/g" \
        -e "s/user = nobody/user = nginx/g" \
        -e "s/group = nobody/group = nginx/g" \
        -e "s/;listen.mode = 0660/listen.mode = 0666/g" \
        -e "s/;listen.owner = nobody/listen.owner = nginx/g" \
        -e "s/;listen.group = nobody/listen.group = nginx/g" \
        -e "s/listen = \/run\/php\/php7.0-fpm.sock/listen = \/var\/run\/php-fpm.sock/g" \
        -e "s/^;clear_env = no$/clear_env = no/" \
        ${fpm_conf} && \
    ln -s /etc/php/7.0/cli/php.ini /etc/php/7.0/cli/conf.d/php.ini && \
    find /etc/php/7.0/cli/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

# Add Scripts
ADD scripts/start.sh /start.sh
RUN chmod 0700 /start.sh

# Source the bash
RUN . ~/.bashrc

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /var/www/html

EXPOSE 80

CMD ["/start.sh"]
