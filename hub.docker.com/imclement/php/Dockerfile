FROM php:5.6-fpm

MAINTAINER Clement Yuan <spyworldxp@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
		libbz2-dev \
		libcurl4-openssl-dev \
		libxml2-dev \
		libenchant-dev \
		libssl-dev \
		libgmp3-dev \
		libicu-dev \
		libldap2-dev \
		libpng-dev \
		libmcrypt-dev \
		unixodbc-dev \
		firebird-dev \
		libpq-dev \
		libsqlite3-dev \
		libpspell-dev \
		libedit-dev \
		librecode-dev \
		libsnmp-dev \
		libtidy-dev \
		libxslt-dev \
		libc-client2007e-dev \
		libkrb5-dev \
		freetds-dev \
		libjpeg62-turbo-dev \
		unzip \
		libfreetype6-dev \
		libsnmp30 \
		curl \
		snmp \
		libaio1 \
		libmemcached-dev \
		libmagickwand-dev \
		poppler-utils \
		ghostscript \
	&& ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
	&& docker-php-source extract \
	&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \
	&& docker-php-ext-install ldap \
	&& docker-php-ext-configure pdo_odbc  --with-pdo-odbc=unixODBC,/usr/ \
	&& docker-php-ext-install pdo_odbc \
	&& docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos \
	&& docker-php-ext-install imap \
	&& docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu \
	&& docker-php-ext-install pdo_dblib \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install xmlreader bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo ftp \
gettext gmp hash intl json mbstring mcrypt mysqli  opcache  pcntl pdo  pdo_firebird pdo_mysql \
pdo_pgsql pdo_sqlite pgsql posix pspell readline recode session shmop simplexml snmp soap sockets \
sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlrpc xmlwriter xsl zip iconv interbase mysql \
	&& curl -O https://raw.githubusercontent.com/davidgaya/docker-apache-php-oci/master/instantclient-basic-linux.x64-12.1.0.2.0.zip \
	&& curl -O https://raw.githubusercontent.com/davidgaya/docker-apache-php-oci/master/instantclient-sdk-linux.x64-12.1.0.2.0.zip \
	&& curl -O https://raw.githubusercontent.com/davidgaya/docker-apache-php-oci/master/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip \
	&& unzip instantclient-basic-linux.x64-12.1.0.2.0.zip -d /usr/local/ \
	&& unzip instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /usr/local/ \
	&& unzip instantclient-sqlplus-linux.x64-12.1.0.2.0.zip -d /usr/local/ \
	&& rm instantclient-basic-linux.x64-12.1.0.2.0.zip \
	&& rm instantclient-sdk-linux.x64-12.1.0.2.0.zip \
	&& rm instantclient-sqlplus-linux.x64-12.1.0.2.0.zip \
	&& ln -s /usr/local/instantclient_12_1 /usr/local/instantclient \
	&& ln -s /usr/local/instantclient/libclntsh.so.12.1 /usr/local/instantclient/libclntsh.so \
	&& ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus \
	&& docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient \
	&& docker-php-ext-install oci8 \
	&& docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/usr/local/instantclient/,12.1 \
	&& docker-php-ext-install pdo_oci \
	&& set -x \
    && cd /usr/src/php/ext/odbc \
    && phpize \
    && sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure \
    && ./configure --with-unixODBC=shared,/usr \
    && docker-php-ext-install odbc \
	&& pecl install xdebug-2.5.5 \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=0" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.cli_color=0" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.profiler_enable=0" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_mode=req" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_host=dockerhost" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini \
	&& cat /usr/local/etc/php/conf.d/xdebug.ini \
	&& php -i | grep xdebug.remote \
	&& pecl install imagick && docker-php-ext-enable imagick \
	&& pecl install memcached-2.2.0 && docker-php-ext-enable memcached \
	&& pecl install redis-4.3.0 && docker-php-ext-enable redis \
	&& pecl install mongodb && docker-php-ext-enable mongodb \
	&& curl -L https://cs.symfony.com/download/php-cs-fixer-v2.phar -o /usr/local/bin/php-cs-fixer \
	&& chmod a+x /usr/local/bin/php-cs-fixer \
	&& curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/bin \
	&& mkdir /.composer \
    && chmod 777 /.composer

ENV PATH /root/.composer/vendor/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/instantclient_12_1/

RUN curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar && chmod +x phpunit.phar && mv phpunit.phar /usr/local/bin/phpunit

RUN apt-get autoremove -y \
 	&& apt-get clean all \
 	&& rm -rf /var/lib/apt/lists/* \
 	&& rm -rf /usr/share/doc /usr/share/man /usr/share/locale \
 	&& rm -rf /usr/src/php \
 	&& rm -rf /tmp/pear \
	&& { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

EXPOSE 9000
CMD ["php-fpm"]
