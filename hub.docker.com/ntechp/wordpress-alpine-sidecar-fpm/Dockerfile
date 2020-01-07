FROM wordpress:fpm-alpine

RUN apk add --no-cache --virtual .build-deps libxml2-dev && \
	apk add --no-cache --virtual .ext-deps libxml2 libzip-dev && \
	export CFLAGS="-I/usr/src/php" && \
	docker-php-ext-install bcmath calendar iconv mysqli opcache pdo_mysql dom xml xmlreader exif hash json posix sockets tokenizer zip && \
	apk del .build-deps && \
	apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
	docker-php-ext-configure gd \
	--with-gd \
	--with-freetype-dir=/usr/include/ \
	--with-png-dir=/usr/include/ \
	--with-jpeg-dir=/usr/include/ && \
	NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
	docker-php-ext-install -j${NPROC} gd && \
	apk del freetype-dev libpng-dev libjpeg-turbo-dev && \
	apk add --no-cache shadow && \
	/usr/sbin/usermod -u 100 www-data && \
	/usr/sbin/groupmod -g 101 www-data && \
	apk del shadow