FROM  php:7-fpm
MAINTAINER Nesterov Alexander <alex19pov31@gmail.com>

RUN rm /etc/localtime && \
	mkdir -p /tmp/php_upload/www && chmod -R 777 /tmp/php_upload/www && \
	ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
	groupadd nginx && useradd -g nginx nginx && apt-get update -y && \
	apt-get install curl wget git msmtp libpng12-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libcurl4-gnutls-dev libxml2-dev memcached libmemcached-dev -y && \
	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
	docker-php-ext-install mbstring iconv mcrypt mysqli opcache xml zip gd && \
	mkdir /tmp/php_sessions/ && mkdir /tmp/php_sessions/www/ && chown -R nginx:nginx /tmp/php_sessions/www/ && \
	cd /tmp && git clone https://github.com/websupport-sk/pecl-memcache && cd /tmp/pecl-memcache && phpize && \
	./configure --disable-all --enable-cli --enable-zlib --enable-hash --enable-session --without-gd --with-bz2 --enable-memcache=shared && \
	make && make install && /usr/local/bin/docker-php-ext-enable memcache && mkdir /home/www && chown -R nginx:nginx /home/www && \
	cd /tmp && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php composer-setup.php && php -r "unlink('composer-setup.php');" && \
	mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer
	
	VOLUME /home/www
	
COPY conf/ /

ENTRYPOINT /bin/bash /root/run.sh