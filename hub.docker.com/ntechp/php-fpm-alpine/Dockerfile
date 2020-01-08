FROM php:7.2-fpm-alpine

RUN apk add --no-cache --virtual .ext-deps libxml2 libzip freetype libpng libjpeg-turbo libxslt icu && \
	apk add --no-cache --virtual .build-deps shadow libxml2-dev libzip-dev freetype-dev libpng-dev libjpeg-turbo-dev libxslt-dev icu-dev g++ && \
	export CFLAGS="-I/usr/src/php" && \
	docker-php-ext-install bcmath calendar iconv mysqli opcache pdo_mysql dom xml xmlreader exif hash json posix sockets tokenizer zip \
		xsl intl soap && \
	docker-php-ext-configure gd \
	--with-gd \
	--with-freetype-dir=/usr/include/ \
	--with-png-dir=/usr/include/ \
	--with-jpeg-dir=/usr/include/ && \
	NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
	docker-php-ext-install -j${NPROC} gd && \
	/usr/sbin/usermod -u 100 www-data && \
	/usr/sbin/groupmod -g 101 www-data && \
	apk del .build-deps