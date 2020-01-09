FROM alpine:3.7
LABEL Maintainer="Jan Ritter <git@janrtr.de>" \
      Description="Lightweight container with Nginx 1.12 & PHP-FPM 7.1 based on Alpine Linux, optimized for Symfony"

# Install packages
RUN apk --no-cache add php7 \
    php7-soap \
	php7-gmp \
	php7-pdo_odbc \
	php7-zip \
	php7-sqlite3 \
	php7-pdo_pgsql \
	php7-bcmath \
	php7-pdo_mysql \
	php7-pdo_sqlite \
	php7-gettext \
	php7-xmlwriter \
	php7-tokenizer \
	php7-xmlrpc \
	php7-bz2 \
	php7-pdo_dblib \
	php7-session \
	php7-redis \
    php7-mcrypt \
    php7-fpm \
    php7-mysqli \
    php7-json \
    php7-openssl\
    php7-curl\
    php7-pdo \
    php7-zlib \
    php7-xml \
    php7-phar \
    php7-intl \
    php7-dom \
    php7-xmlreader \
    php7-ctype \
    php7-mbstring \
    php7-gd \
    nginx \
    supervisor \
    curl

#Configure nginx user
RUN adduser -D -u 1000 -g 'www' www

#Add nginx web folder
RUN mkdir /www
RUN chown -R www:www /var/lib/nginx
RUN chown -R www:www /www

# Configure nginx
COPY config/nginx.conf /etc/nginx/nginx.conf

# Copy self signed cert
COPY cert/server.crt /etc/nginx/server.crt
COPY cert/server.key /etc/nginx/server.key

# Configure PHP-FPM
COPY config/fpm-pool.conf /etc/php7/php-fpm.d/zzz_custom.conf
COPY config/php.ini /etc/php7/conf.d/zzz_custom.ini

# Configure supervisord
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Add Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Add application
RUN mkdir -p /www/symfony
WORKDIR /www/symfony
COPY src/ /www/symfony/web/

EXPOSE 80 443
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
