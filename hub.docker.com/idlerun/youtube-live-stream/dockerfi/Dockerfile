FROM php:5.6-fpm

MAINTAINER Aklis <aklis@qq.com>
#The php container is only to execute php script

COPY fpm/* /usr/local/etc/
COPY php/* /usr/local/etc/php/conf.d/

RUN apt-get update && apt-get install -y wget libmemcached-dev libssl-dev libpng12-dev libjpeg-dev re2c libfreetype6-dev libmcrypt-dev libxml2-dev libpq-dev --no-install-recommends && rm -r /var/lib/apt/lists/*
RUN wget https://pecl.php.net/get/redis-2.2.7.tgz -O /tmp/redis.tgz

# Maybe you need the follows
#bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mcrypt mssql mysql mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop simplexml snmp soap sockets spl standard sybase_ct sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zip
RUN docker-php-ext-configure gd --with-jpeg-dir --with-png-dir --with-freetype-dir \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install mysql \
	&& docker-php-ext-install iconv \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install mbstring \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install bcmath \
	#&& docker-php-ext-install xdebug \
	#&& docker-php-ext-install memcache \
	#&& docker-php-ext-install xhprof \
	#&& docker-php-ext-install mongo \
	#&& docker-php-ext-install memcached \
	&& docker-php-ext-install pgsql \
	&& docker-php-ext-install pdo_pgsql \
	&& docker-php-ext-install opcache \
	&& pecl install /tmp/redis.tgz \
	&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

WORKDIR /opt

CMD ["php-fpm"]
