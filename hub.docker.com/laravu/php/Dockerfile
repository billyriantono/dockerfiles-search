###
# laravu
#
# Repository:    PHP
# Image:         CLI/Base
# Version:       7.1.x
# Base distro:   Alpine 3.6
#
FROM alpine:3.6

LABEL version="0.2.17-dbg"
LABEL description="Php-FPM for LaraVu"
LABEL maintainer="4ngo.ru@gmail.com"

ENV FRAMEWORK=laravel \
    XDEBUG_ENABLED=true \
    TIMEZONE=Europe/Kiev \
    TERM=xterm-256color \
    COLORTERM=truecolor \
    COMPOSER_PROCESS_TIMEOUT=1200

# Add the ENTRYPOINT script
ADD start.sh /scripts/start.sh
ADD settz.sh /scripts/settz.sh
ADD bashrc /home/laravu/.bashrc

# Install PHP From DotDeb, Common Extensions, Composer and then cleanup
RUN echo "---> Enabling PHP-Alpine" && \
    apk add --update wget && \
    wget -O /etc/apk/keys/php-alpine.rsa.pub http://php.codecasts.rocks/php-alpine.rsa.pub && \
    echo "@php http://php.codecasts.rocks/v3.6/php-7.1" >> /etc/apk/repositories && \
    apk add --update \
    curl \
    bash \
    fontconfig \
    libxrender \
    libxext \
    nano \
    git \
    unzip \
    wget \
    make \
    sudo && \
    echo "---> Preparing and Installing PHP" && \
    apk add --update \
    php7@php \
    php7-apcu@php \
    php7-bcmath@php \
    php7-bz2@php \
    php7-calendar@php \
    php7-curl@php \
    php7-ctype@php \
    php7-exif@php \
    php7-fpm@php \
    php7-gd@php \
    php7-iconv@php \
    php7-imagick@php \
    php7-imap@php \
    php7-intl@php \
    php7-json@php \
    php7-mbstring@php \
    php7-mcrypt@php \
    php7-mysqlnd@php \
    php7-pdo_mysql@php \
    php7-opcache@php \
    php7-posix@php \
    php7-redis@php \
    php7-soap@php \
    php7-sqlite3@php \
    php7-xdebug@php \
    php7-xml@php \
    php7-xmlreader@php \
    php7-openssl@php \
    php7-phar@php \
    php7-zip@php \
    php7-zlib@php \
    php7-phpdbg@php && \
    sudo ln -s /usr/bin/php7 /usr/bin/php && \
    echo "---> Installing Composer" && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    echo "---> Cleaning up" && \
    rm -rf /tmp/* && \
    echo "---> Adding the www-data user" && \
    adduser -D -u 82 www-data && \
    mkdir -p /var/www && \
    echo "---> Adding the laravu user" && \
    adduser -D -u 1000 laravu && \
#    chown -R www-data:www-data /var/www && \
    chown -R laravu:laravu /var/www && \
    echo "laravu  ALL = ( ALL ) NOPASSWD: ALL" >> /etc/sudoers && \
    echo "---> Configuring PHP" && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php7/php-fpm.conf  && \
    sed -i "/pid = .*/c\;pid = /run/php/php7.1-fpm.pid" /etc/php7/php-fpm.conf && \
    sed -i "/;daemonize = .*/c\daemonize = yes" /etc/php7/php-fpm.conf && \
    sed -i "/error_log = .*/c\error_log = /proc/self/fd/2" /etc/php7/php-fpm.conf && \
    sed -i "/post_max_size = .*/c\post_max_size = 1000M" /etc/php7/php.ini && \
    sed -i "/upload_max_filesize = .*/c\upload_max_filesize = 1000M" /etc/php7/php.ini && \
    sed -i "/zend_extension=xdebug.so/c\;zend_extension=xdebug.so" /etc/php7/conf.d/00_xdebug.ini && \
    chown -R laravu:laravu /home/laravu && \
    chmod -R 755 /scripts && \
    /scripts/settz.sh && \
#    chmod +x /scripts/start.sh && \
    rm -rf /tmp/*
#    rm -rf /etc/php7/php-fpm.d/*

ADD ./conf/laravel.ini /etc/php7/conf.d/30_laravel.ini
ADD ./conf/www.conf /etc/php7/php-fpm.d/www.conf

# Define the running user
USER laravu
#USER www-data

# Application directory
WORKDIR "/var/www"

# Environment variables
ENV PATH=/home/laravu/.composer/vendor/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# As non daemon and single base image, it may be used as cli container
EXPOSE 9000
# Define the entry point that tries to enable newrelic
ENTRYPOINT ["/scripts/start.sh"]
#CMD ["php-fpm7"]
#CMD ["/scripts/start.sh"]
