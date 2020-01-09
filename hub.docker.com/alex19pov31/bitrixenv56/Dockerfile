FROM  php:5.6-fpm
MAINTAINER Nesterov Alexander <alex19pov31@gmail.com>

RUN rm /etc/localtime && \
	ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
	apt-get update -y && apt-get install wget curl git -y && \
	cd /tmp && wget http://nginx.org/keys/nginx_signing.key && \
	apt-key add nginx_signing.key && \
	echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list && \
	echo "deb-src http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list && \
	apt-get install software-properties-common -y && \
	apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xcbcb082a1bb943db && \
	add-apt-repository 'deb [arch=amd64,i386] http://mirror.timeweb.ru/mariadb/repo/10.1/debian jessie main' && \
	apt-get update -y && \
	echo 'mariadb-server-10.1 mysql-server/root_password password 1234567' | debconf-set-selections && \
	echo 'mariadb-server-10.1 mysql-server/root_password_again password 1234567' | debconf-set-selections && \
	echo 'mariadb-server-10.0 mysql-server/root_password password 1234567' | debconf-set-selections && \
	echo 'mariadb-server-10.0 mysql-server/root_password_again password 1234567' | debconf-set-selections && \
	apt-get install nginx mariadb-server curl wget git msmtp libpng12-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libcurl4-gnutls-dev libxml2-dev memcached libmemcached-dev -y && \
	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
	docker-php-ext-install mbstring iconv mcrypt mysql mysqli opcache xml zip gd && \
	pecl install memcached && docker-php-ext-enable memcached && \
	mkdir /tmp/php_sessions/ && mkdir /tmp/php_sessions/www/ && chown -R nginx:nginx /tmp/php_sessions/www/
	
COPY conf/ /
EXPOSE 80
EXPOSE 443

ENTRYPOINT /bin/bash /root/run.sh