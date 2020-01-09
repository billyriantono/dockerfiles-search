FROM alpine:3.4

RUN addgroup -S www-data \
 && adduser -D -S -G www-data -s /usr/sbin/nologin -h /var/www www-data \
 && apk add --no-cache --update php5-fpm \
	php5-curl \
	php5-ctype \
	php5-dom \
	php5-ftp \
	php5-iconv \
	php5-json \
	php5-openssl \
	php5-pdo_sqlite \
	php5-phar \
	php5-posix \
	php5-sqlite3 \
	php5-xml \
	php5-xmlreader \
	php5-zlib

COPY php-fpm.conf /etc/php5/php-fpm.conf

EXPOSE 9000

CMD [ "/usr/bin/php-fpm" ]

