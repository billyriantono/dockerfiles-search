FROM php:7.1.3-fpm
MAINTAINER Dmitry Kuzmin rockwith@me.com

RUN DEBIAN_FRONTEND=noninteractive \
	apt-get update;\
	apt-get -y install mc;\
	apt-get -y install software-properties-common


##-------------MSSQL--------------- OLD without mssql native support
#RUN echo "\r\n deb http://ftp.de.debian.org/debian/ sid main" >> /etc/apt/sources.list && \
#    apt-get update && \
#    apt-get -y install freetds-common freetds-bin unixodbc php7.1-sybase && \
#    cp /usr/lib/php/20160303/pdo_dblib.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/ && \
#    cp /etc/php/7.1/mods-available/pdo_dblib.ini /usr/local/etc/php/conf.d/ && \
#    sed -i '$ d' /etc/apt/sources.list


#-------------LDAP---------------

RUN apt-get update && \
	apt-get install -y libldap2-dev && \
	docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
	docker-php-ext-install ldap

#-------------OTHER_EXT----------------

RUN apt-get install -y --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libjpeg-dev \
    libpng12-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev

RUN pecl channel-update pecl.php.net && \
    docker-php-ext-install mcrypt && \
	docker-php-ext-install zip && \
	docker-php-ext-install tokenizer && \
  	docker-php-ext-install pdo_mysql && \
  	docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd




#-------------XDEBUG----------------

ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    # Install the xdebug extension
    pecl install xdebug && \
    docker-php-ext-enable xdebug \
;fi




##---------------MSSQL----------------
RUN echo "\r\n deb http://ftp.de.debian.org/debian/ sid main" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install tdsodbc php7.1-sybase
# libsybdb5 мы соберём сами
RUN apt-get -y install gcc
RUN apt-get -y install build-essential

ADD freetds-patched.tar /temp/
RUN cd /temp/freetds-1.00.27 && \
	./configure --enable-msdblib --prefix=/usr/local && \
	make -j$(nproc) && \
	make install
RUN docker-php-ext-install pdo_dblib #можно и без mssql
#уберём за собой
RUN sed -i '$ d' /etc/apt/sources.list





ADD xdebug.ini /usr/local/etc/php/conf.d/
ADD php.ini /usr/local/etc/php/

ADD freetds.conf /usr/local/etc

CMD ["php-fpm"]
EXPOSE 9000
