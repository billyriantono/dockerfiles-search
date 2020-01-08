FROM php:7.2-cli

ARG TIMEZONE=Europe/Berlin

RUN unlink /etc/localtime && ln -s /usr/share/zoneinfo/${TIMEZONE} /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata
RUN echo "date.timezone=`cat /etc/timezone`" > /usr/local/etc/php/conf.d/timezone.ini

RUN apt-get -qq update && \
	apt-get -qq install --no-install-recommends --no-install-suggests -y \
	vim less wget curl procps openssh-client rsync locales \
	zip unzip git \
	libgd3 libgd-dev freetype* libjpeg-dev libpng-dev libzip-dev \
	libmcrypt-dev \
	zlib1g-dev libicu-dev \
	libxml2-dev && \
	apt-get autoremove -y && apt-get clean -y

RUN docker-php-ext-install bcmath
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install iconv
RUN docker-php-ext-install intl
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install opcache
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip

# https://pecl.php.net/package/mcrypt
RUN yes '' | pecl install mcrypt-1.0.2 && \
	echo extension="mcrypt.so" > /usr/local/etc/php/conf.d/php-ext-mcrypt.ini

RUN curl --silent --show-error https://getcomposer.org/installer > composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin
RUN ln -s /usr/local/bin/composer.phar /usr/local/bin/composer
