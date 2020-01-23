FROM alpine:3.5

# Repository/Image Maintainer
MAINTAINER Ahgora Sistemas

# Variables for enabling NewRelic
ENV XDEBUG_ENABLED=false \
    NR_ENABLED=false \
    NR_APP_NAME="" \
    NR_LICENSE_KEY="" \
    TERM=xterm-256color \
    COLORTERM=truecolor \
    COMPOSER_PROCESS_TIMEOUT=1200

# Install PHP From DotDeb, Common Extensions, Composer and then cleanup
RUN echo "---> Enabling PHP-Alpine" && \
    wget -O /etc/apk/keys/php-alpine.rsa.pub \
    http://php.codecasts.rocks/php-alpine.rsa.pub && \
    echo "http://php.codecasts.rocks/7.1" >> /etc/apk/repositories && \
    apk add --update \
    curl \
    bash \
    fontconfig \
    libxrender \
    libxext \
    nano \
    vim \
    git \
    unzip \
    wget \
    sudo && \
    echo "---> Preparing and Installing PHP" && \
    apk add --update \
    php7 \
    php7-apcu \
    php7-bcmath \
    php7-bz2 \
    php7-curl \
    php7-ctype \
    php7-exif \
    php7-fpm \
    php7-gd \
    php7-imagick \
    php7-imap \
    php7-intl \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-mysqlnd \
    php7-pdo_mysql \
    php7-mongodb \
    php7-opcache \
    php7-pdo_pgsql \
    php7-pgsql \
    php7-redis \
    php7-soap \
    php7-sqlite3 \
    php7-xdebug \
    php7-xml \
    php7-xmlreader \
    php7-openssl \
    php7-phar \
    php7-zip \
    php7-zlib \
    php7-phpdbg && \
    sudo ln -s /usr/bin/php7 /usr/bin/php && \
    echo "---> Installing Composer" && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    echo "---> Cleaning up" && \
    rm -rf /tmp/* && \
    wget -O /tini https://github.com/krallin/tini/releases/download/v0.14.0/tini-static && \
    chmod +x /tini && \
    echo "---> Configuring PHP" && \
    sed -i "/listen = .*/c\listen = [::]:9000" /etc/php7/php-fpm.d/www.conf && \
    sed -i "/;access.log = .*/c\access.log = /proc/self/fd/2" /etc/php7/php-fpm.d/www.conf && \
    sed -i "/;clear_env = .*/c\clear_env = no" /etc/php7/php-fpm.d/www.conf && \
    sed -i "/;catch_workers_output = .*/c\catch_workers_output = yes" /etc/php7/php-fpm.d/www.conf && \
    sed -i "/pid = .*/c\;pid = /run/php/php7.1-fpm.pid" /etc/php7/php-fpm.conf && \
    sed -i "/;daemonize = .*/c\daemonize = yes" /etc/php7/php-fpm.conf && \
    sed -i "/error_log = .*/c\error_log = /proc/self/fd/2" /etc/php7/php-fpm.conf && \
    sed -i "/post_max_size = .*/c\post_max_size = 1000M" /etc/php7/php.ini && \
    sed -i "/upload_max_filesize = .*/c\upload_max_filesize = 1000M" /etc/php7/php.ini && \
    sed -i "/zend_extension=xdebug.so/c\;zend_extension=xdebug.so" /etc/php7/conf.d/00_xdebug.ini && \
    rm -rf /tmp/*


# Application directory
WORKDIR "/var/www/app"

# Installs Caddy
RUN curl https://getcaddy.com | bash

# Installs Confd
RUN wget https://github.com/kelseyhightower/confd/releases/download/v0.12.0-alpha3/confd-0.12.0-alpha3-linux-amd64 -O /usr/local/bin/confd && \
    chmod +x /usr/local/bin/confd && \
    mkdir -p /etc/confd/conf.d /etc/confd/templates

# As non daemon and single base image, it may be used as cli container
CMD ["/bin/bash"]
