FROM gliderlabs/alpine:latest

EXPOSE 9000

RUN apk-install \
        php-mcrypt \
        php-intl \
        php-pdo_mysql \
        php-fpm \
        php-opcache \
        php-mysql \
        php-ctype \
        php-xml \
        php-xmlreader \
        php-xmlrpc \
        php-curl \
        php-openssl \
        php-gd \
        php-exif \
        php-json \
        php-zip \
	    php-sockets \
	    php-pgsql \
        php-ldap \
        php-zlib \
	    php-pdo_pgsql && \
    sed -i 's/listen = 127.0.0.1:9000/listen = 0.0.0.0:9000/g' /etc/php/php-fpm.conf && \
    sed -i 's/listen.allowed_clients = 127.0.0.1/;listen.allowed_clients = 127.0.0.1/g' /etc/php/php-fpm.conf
CMD ["php-fpm","-F"]
