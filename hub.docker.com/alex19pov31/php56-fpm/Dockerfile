FROM  php:5.6-fpm
MAINTAINER Nesterov Alexander <alex19pov31@gmail.com>

RUN rm /etc/localtime && \
	mkdir -p /tmp/php_upload/www && chmod -R 777 /tmp/php_upload/www && \
	ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
	groupadd nginx && useradd -g nginx nginx && apt-get update -y && \
	apt-get install curl wget git msmtp libpng12-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libcurl4-gnutls-dev libxml2-dev memcached libmemcached-dev -y && \
	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
	docker-php-ext-install mbstring iconv mcrypt mysql mysqli opcache xml zip gd && \
	pecl install memcache && docker-php-ext-enable memcache && \
	mkdir /tmp/php_sessions/ && mkdir /tmp/php_sessions/www/ && chown -R nginx:nginx /tmp/php_sessions/www/ && \
	cd /tmp && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php composer-setup.php && php -r "unlink('composer-setup.php');" && \
	mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

	VOLUME /home/www
	
COPY conf/ /

ENTRYPOINT /bin/bash /root/run.sh