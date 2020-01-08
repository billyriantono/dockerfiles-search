FROM php:7.1-fpm
MAINTAINER Siddhy NDiaye

RUN apt-get -y update && \
    apt-get -y install git libcurl4-gnutls-dev libmcrypt-dev libpng12-dev libxml2-dev libxslt-dev vim-nox mysql-client ssmtp && \
    apt-get -y install libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libghc-text-icu-dev bsd-mailx && \
    apt-get -y install pkg-config libssl-dev locales && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen fr_FR.UTF-8 && \
    /usr/sbin/update-locale LANG=fr_FR.UTF-8 && \
    pecl install mongodb && \
    echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini && \
    docker-php-ext-enable mongodb && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) curl bcmath gd mcrypt mysqli opcache pdo_mysql soap xsl zip iconv gd intl mbstring xmlwriter && \
    apt-get -y clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer --version

COPY    ssmtp.conf /etc/ssmtp/ssmtp.conf
COPY    revaliases /etc/ssmtp/revaliases