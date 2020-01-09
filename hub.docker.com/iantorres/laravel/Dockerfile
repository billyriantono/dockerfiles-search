FROM php:7-apache-stretch

MAINTAINER Ian Torres <iantorres@outlook.com>
LABEL maintainer="Ian Torres <iantorres@outlook.com>" \
        php="7.3"

RUN BUILD_DEPENDENCIES="autoconf" \
    DEV_DEPENDENCIES="libcurl4-gnutls-dev \
            libzip-dev \
     	    libicu-dev \
     	    libmcrypt-dev \
     	    libreadline-dev \
     	    libvpx-dev \
     	    libjpeg-dev \
     	    libpng-dev \
     	    libxpm-dev \
     	    zlib1g-dev \
     	    libfreetype6-dev \
     	    libxml2-dev \
     	    libexpat1-dev \
     	    libbz2-dev \
     	    libgmp3-dev \
     	    libldap2-dev \
     	    unixodbc-dev \
     	    libpq-dev \
     	    libsqlite3-dev \
     	    libaspell-dev \
     	    libsnmp-dev \
     	    libpcre3-dev \
    	    libtidy-dev \
    	    openssh-client \
    	    iputils-ping \
    	    git \
    	    zip \
    	    unzip \
    	    chromedriver" \
    && docker-php-source extract \
    && apt-get update && apt-get install -y \
            $BUILD_DEPENDENCIES \
            $DEV_DEPENDENCIES \
    && docker-php-ext-install mbstring pdo_mysql curl json intl exif gd xml zip bz2 opcache bcmath soap tidy pcntl ctype \
    && php -v \
    && ping -c 3 localhost

RUN cd ~ \
    && EXPECTED_SIGNATURE=$(curl -q -sS https://composer.github.io/installer.sig) \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && ACTUAL_SIGNATURE=$(php -r "echo hash_file('SHA384', 'composer-setup.php');") \
    && if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]; then >&2 echo 'ERROR: Invalid installer signature' && rm composer-setup.php && exit 1; fi \
    && php composer-setup.php --quiet --install-dir=/usr/local/bin --filename=composer \
    && RESULT=$? \
    && composer --version \
    && rm composer-setup.php \
    && docker-php-source delete

RUN composer global require hirak/prestissimo
