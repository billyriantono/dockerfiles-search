FROM php:7.0-fpm-alpine as builder
RUN apk add --no-cache bzip2-dev coreutils sqlite-dev libxml2-dev curl-dev gmp-dev icu-dev libpng-dev jpeg-dev freetype-dev autoconf imagemagick-dev gcc libc-dev rabbitmq-c-dev make libtool \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include \
	&& docker-php-ext-install -j$(nproc) bcmath pdo pdo_mysql pdo_sqlite mbstring json xml zip curl gmp intl \
	    gd soap sockets pcntl bz2 \
	&& pecl install imagick \
	&& pecl install amqp \
	&& pecl install apcu \
	&& docker-php-ext-enable imagick

FROM php:7.0-fpm-alpine

COPY --from=builder /usr/local/lib/php/extensions/no-debug-non-zts-20151012 /usr/local/lib/php/extensions/no-debug-non-zts-20151012

COPY confd /etc/confd
ADD https://github.com/kelseyhightower/confd/releases/download/v0.10.0/confd-0.10.0-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd \
	&& apk add --no-cache bash sqlite libxml2 curl gmp icu libpng jpeg freetype imagemagick gcc ssmtp libmcrypt-dev rabbitmq-c \
	# Fix alpine iconv problems part 1
	# See https://github.com/docker-library/php/issues/240
	&& apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community gnu-libiconv \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-enable bz2 bcmath pdo pdo_mysql pdo_sqlite mbstring json xml zip curl gmp intl gd imagick soap mcrypt \
	    amqp sockets pcntl apcu

#mcrypt predis imagick

# Fix alpine iconv problems part 2
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so

COPY docker-php-entrypoint /usr/local/bin/

COPY wait-for-it /usr/local/bin/wait-for-it

ENTRYPOINT ["docker-php-entrypoint"]
CMD "php-fpm"
