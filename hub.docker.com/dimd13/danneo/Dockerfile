FROM php:5.6-apache

RUN apt-get update; \
	apt-get install -y \
		curl \
		libcurl3 \
		libcurl3-dev \
	    rsync \
		libjpeg-dev \
		libpng-dev \
		unzip \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd mysqli zip mbstring json curl

RUN a2enmod rewrite expires

VOLUME /var/www/html

COPY danneo.zip /tmp

RUN cd /tmp && \
	unzip -qq danneo.zip 'www/*' -d /usr/src/danneo/ && \
	rm danneo.zip && \
	chown -R www-data:www-data /usr/src/danneo/

ENV DATE_TZ	Europe/Moscow
ENV MAX_EXECUTION_TIME	30
ENV POST_MAX_SIZE	8M
ENV UPLOAD_MAX_FILESIZE	2M
ENV MEMORY_LIMIT	128M
ENV ALLOW_URL_FOPEN	Off

COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["apache2-foreground"]