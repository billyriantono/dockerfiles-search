FROM buddyingdevelopment/amazonlinux:2
MAINTAINER buddyingdevelopment <development@buddying.jp>

RUN yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm \
 && yum-config-manager --enable remi-php72

RUN yum update -y
RUN yum install -y \
    httpd \
    mod_ssl

RUN yum install -y \
    php72 \
    php72-php \
    php72-php-common \
    php72-php-ctype \
    php72-php-curl \
    php72-php-devel \
    php72-php-fileinfo \
    php72-php-gd \
    php72-php-hash \
    php72-php-intl \
    php72-php-json \
    php72-php-libxml \
    php72-php-mbstring \
    php72-php-mcrypt \
    php72-php-mysqlnd \
    php72-php-openssl \
    php72-php-opcache \
    php72-php-pdo \
    php72-php-pecl-apcu \
    php72-php-posix \
    php72-php-phar \
    php72-php-session \
    php72-php-simplexml \
    php72-php-soap \
    php72-php-xml \
    php72-php-xmlwriter \
    php72-php-xsl \
    php72-php-zip \
    php72-php-zlib \
    php72-php-pecl-memcached \
    php72-php-pecl-mongodb

RUN ln -s /usr/bin/php72 /usr/bin/php

RUN yum install -y postfix

RUN rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && yum clean all

# Settings
COPY ./setup/httpd_development.conf /etc/httpd/conf.d/
COPY ./setup/ssl.conf /etc/httpd/conf.d/ssl.conf
COPY ./setup/php_development.ini /etc/opt/remi/php72/php.d/
COPY ./setup/entrypoint.sh /

# Directory, permission, ... 
RUN rm -rf /var/www/* \
 && mkdir /var/www/html \
 && mkdir /var/log/php \
 && chmod 777 -R /var/log/php \
 && chmod 777 -R /var/opt/remi/php72/lib/php/session \
 && usermod -u 1000 apache \
 && groupmod -g 1000 apache \
 && sed -i.dist 's,^#ServerName.*$,ServerName 127.0.0.1:80,g' /etc/httpd/conf/httpd.conf \
 && sed -i.dist 's/^inet_interfaces = localhost$/inet_interfaces = all/g' /etc/postfix/main.cf \
 && chmod 700 /entrypoint.sh

# Composer
RUN curl -sS https://getcomposer.org/installer | php72 -- --install-dir=/usr/local/bin --filename=composer

# Environment
ENV HOME=/root
WORKDIR /var/www

# Listen
EXPOSE 80

ENTRYPOINT /entrypoint.sh