# PHP 5.6.14 Image 
#
# VERSION               0.0.1

FROM mateusmiranda/ubuntu

MAINTAINER Mateus Miranda <mateusmiranda@gmail.com>

RUN apt-get update && apt-get -y install wget vim git bzip2 net-tools

RUN mkdir ~/php-src && mkdir ~/php-src-memcache && mkdir ~/php-src-xdebug

RUN cd ~/php-src && wget http://us2.php.net/get/php-5.6.14.tar.bz2/from/this/mirror -O php-5.6.14.tar.bz2 \
	&& tar -xvjf php-5.6.14.tar.bz2 -C ~/php-src

RUN cd ~/php-src-memcache && wget http://pecl.php.net/get/memcache-2.2.6.tgz -O memcache-2.2.6.tgz \
        && tar -zxvf memcache-2.2.6.tgz -C ~/php-src-memcache

RUN cd ~/php-src-xdebug && wget http://xdebug.org/files/xdebug-2.3.3.tgz -O xdebug-2.3.3.tgz \
        && tar -zxvf xdebug-2.3.3.tgz -C ~/php-src-xdebug

RUN apt-get -y install build-essential autoconf libtool libxml2 libxml2-dev openssl libcurl4-openssl-dev  \
    libbz2-1.0 libbz2-dev libjpeg-dev libpng12-dev libfreetype6 libfreetype6-dev \
    libldap-2.4-2 libldap2-dev libmcrypt4 libmcrypt-dev libmysqlclient-dev \
    libxslt1.1 libxslt1-dev libxt-dev curl

RUN cd ~/php-src/php-5.6.14 && ./configure \
        --enable-fpm \
        --enable-pdo \
        --with-pdo-mysql \
        --enable-sockets \
        --enable-exif \
        --enable-soap \
        --enable-ftp \
        --enable-wddx \
        --enable-pcntl \
        --enable-soap \
        --enable-bcmath \
        --enable-mbstring \
        --enable-dba \
        --enable-gd-native-ttf \
        --enable-zip \
        --enable-calendar \
        --with-mysql \
        --with-mysqli \
        --with-pdo-sqlite \
        --with-iconv \
        --with-zlib \
        --with-bz2 \
        --with-gettext \
        --with-xmlrpc \
        --with-openssl \
        --with-mhash \
        --with-mcrypt \
        --with-xsl \
        --with-curl \
        --with-pcre-regex \
        --with-gd \
        --with-freetype-dir=/usr \
        --with-jpeg-dir=/usr \
        --with-png-dir=/usr \
        --with-ldap \
        --with-pear \
        --with-fpm-user=www-data \
        --with-fpm-group=www-data \
        --with-config-file-path=/etc/php/ \
        --with-config-file-scan-dir=/etc/php/conf.d/ \
        --with-libdir=lib/x86_64-linux-gnu

RUN cd ~/php-src/php-5.6.14 && make install \
	&& mkdir -p /etc/php \
	&& cp php.ini-production /etc/php/php.ini \
	&& cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm \
	&& chmod +x /etc/init.d/php-fpm \
	&& update-rc.d php-fpm defaults \
	&& cp /usr/local/etc/php-fpm.conf.default /usr/local/etc/php-fpm.conf

RUN cd ~/php-src-memcache/memcache-2.2.6 && \
	phpize	&& \
	./configure --enable-memcache && \
	make && \
	mkdir /usr/local/lib/php/modules \
        && cp modules/memcache.so /usr/local/lib/php/modules/memcache.so

RUN cd ~/php-src-xdebug/xdebug-2.3.3 && \
	phpize && \
	./configure --enable-xdebug && \
	make && \
	make install

RUN sed -i 's/listen = 127.0.0.1:9000/listen = 9000/g' /usr/local/etc/php-fpm.conf && \
	sed -i 's/daemonize = yes/daemonize = no/g' /usr/local/etc/php-fpm.conf && \
	sed -i 's/display_errors = Off/display_errors = On/g' /etc/php/php.ini && \
	sed -i "s/;date.timezone =/date.timezone = America\/Sao_Paulo/" /etc/php/php.ini && \
	echo "extension=/usr/local/lib/php/modules/memcache.so" >> /etc/php/php.ini && \
	sed -i 's/short_open_tag = Off/short_open_tag = On/g' /etc/php/php.ini && \
	echo "[xdebug]" >> /etc/php/php.ini && \
        echo "xdebug.default_enable=1" >> /etc/php/php.ini && \
        echo "xdebug.remote_enable=1" >> /etc/php/php.ini && \
        echo "xdebug.remote_handler=dbgp" >> /etc/php/php.ini && \
        echo "xdebug.remote_host=localhost" >> /etc/php/php.ini && \
        echo "xdebug.remote_port=18000" >> /etc/php/php.ini && \
        echo "xdebug.remote_autostart=1" >> /etc/php/php.ini && \
        echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" >> /etc/php/php.ini

#remove source
RUN rm -R ~/php-src && rm -R ~/php-src-memcache && rm -R ~/php-src-xdebug

EXPOSE 9000

CMD ["php-fpm","-F"]
