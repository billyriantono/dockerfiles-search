FROM alpine
MAINTAINER Sergey Turguzov <s.turguzov@gmail.com>

WORKDIR /app

ENV RA_VERSION 4.2.0
ENV COMPOSER_VERSION 1.8.5

RUN apk --update upgrade && apk update && apk add curl ca-certificates && update-ca-certificates --fresh && apk add openssl \
	&& apk --update add \
		--repository http://mirror.yandex.ru/mirrors/alpine/edge/main \
		--repository http://mirror.yandex.ru/mirrors/alpine/edge/community \
	nginx \
	gzip \
	git \
	php7 \
	php7-dom \
	php7-ctype \
	php7-curl \
	php7-fpm \
	php7-gd \
	php7-intl \
	php7-json \
	php7-mbstring \
	php7-mcrypt \
	php7-mysqli \
	php7-mysqlnd \
	php7-opcache \
	php7-pdo \
	php7-pdo_mysql \
	php7-posix \
	php7-session \
	php7-xml \
	php7-iconv \
	php7-phar \
	php7-openssl \
	php7-zip \
	php7-zlib \
	&& wget -qO- https://download.revive-adserver.com/revive-adserver-$RA_VERSION.tar.gz | tar xz --strip 1 \
	&& rm -rf /var/cache/apk/* \
	&& rm -f composer.lock \
	&& wget -q https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar \
	&& php composer.phar install \
	&& chown -R nobody:nobody . \
	&& rm -f composer.phar \
	&& mkdir -p /run/nginx \
	&& chown -R nobody:nobody /var/tmp/nginx
	
COPY nginx/nginx.conf /etc/nginx/nginx.conf

COPY php/php.ini /etc/php7/php.ini
COPY php/www.conf /etc/php7/php-fpm.d/www.conf

EXPOSE 4565

CMD php-fpm7 && nginx -g 'daemon off;'
