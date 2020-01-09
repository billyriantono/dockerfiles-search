FROM php:7-fpm
MAINTAINER Javier Caride "javier.caride@gmail.com"
ENV REFRESHED_AT 2016-02-22

# Install modules
RUN apt-get update \
	&& apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev bzip2 libzip2 libbz2-dev libicu-dev icu-devtools libssl-dev libxslt1-dev libtidy-dev libc-client-dev libkrb5-dev \
	&& docker-php-ext-install iconv mcrypt pdo_mysql bcmath bz2 calendar exif intl ftp mbstring mysqli opcache shmop sockets soap tidy xsl \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install gd \
	&& docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install imap \	
	&& echo "Europe/Madrid" > /etc/timezone \
	&& dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y librabbitmq1 librabbitmq-dev libpcre3-dev zlib1g zlib1g-dev libmemcached-dev \
	&& pecl install amqp \
	&& pecl install oauth \
	&& pecl install gender \
	&& pecl install xdebug \
	&& pecl install mongodb

COPY amqp.ini /usr/local/etc/php/conf.d/amqp.ini
COPY gender.ini //usr/local/etc/php/conf.d/gender.ini
COPY mongodb.ini /usr/local/etc/php/conf.d/mongodb.ini
COPY oauth.ini /usr/local/etc/php/conf.d/oauth.ini
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

VOLUME /webapp
VOLUME /xdebug/log
VOLUME /xdebug/profiling

CMD ["php-fpm"]
