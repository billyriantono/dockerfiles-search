FROM php:5.6-fpm

#Install essential stuff
#git are required by composer
#vim is usefull for debug container in interactive shell
RUN apt-get update && apt-get install -y \
	git \
	vim \
	telnet \ 
	bzip2 \
	libbz2-dev \
	libfreetype6-dev \ 
	libjpeg62-turbo-dev \ 
	libmcrypt-dev \ 
	libpng12-dev \ 
	libghc-postgresql-libpq-dev \ 
	&& docker-php-ext-install mcrypt mbstring bz2 zip \ 
	&& docker-php-ext-configure gd -with-freetype-dir=/usr/include/ -with-jpeg-dir=/usr/include/ \ 
	&& docker-php-ext-configure pgsql -with-pgsql=/usr/include/postgresql/ \ 
	&& docker-php-ext-install gd pgsql pdo_pgsql

RUN curl -sS https://pecl.php.net/get/SPL_Types-0.4.0.tgz -o SPL_Types-0.4.0.tgz  \
    && mkdir -p /usr/src/php/spl \
    && tar -xof SPL_Types-0.4.0.tgz -C /usr/src/php/spl --strip-components=1 \
    && rm SPL_Types-0.4.0.tgz \
    && cd /usr/src/php/spl \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && echo "extension=spl_types.so" > /usr/local/etc/php/conf.d/ext-spl.ini

#Install composer
RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/bin/composer
