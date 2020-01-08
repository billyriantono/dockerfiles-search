# Get latest Alpine distro.
FROM alpine:latest

# Details.
LABEL com.johnnyhuy.version="1.1.0"
LABEL com.johnnyhuy.author="Johnny Huynh"
LABEL com.johnnyhuy.author-email="info@johnnyhuy.com"
LABEL com.johnnyhuy.release-date="2017-12-08"

# Environment variables.
ENV TIMEZONE            Australia/Melbourne
ENV PHP_MEMORY_LIMIT    512M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M

# Update existing packages.
RUN apk update && apk upgrade

# PHP.
RUN \
    echo -e "\nInstalling PHP 7..." \
    && apk add --update \
    php7-bcmath \
    php7-bz2 \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-fpm \
    php7-gd \
    php7-gettext \
    php7-gmp \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-mysqli \
    php7-odbc \
    php7-openssl \
    php7-pdo \
    php7-pdo_dblib \
    php7-pdo_mysql \
    php7-pdo_odbc \
    php7-pdo_pgsql \
    php7-pdo_sqlite \
    php7-session \
    php7-soap \
    php7-sqlite3 \
    php7-tokenizer \
    php7-xml \
    php7-xmlreader \
    php7-xmlrpc \
    php7-xmlwriter \
    php7-zip \
    php7-zlib \
    && sed -i "s|;*daemonize\s*=\s*yes|daemonize = no|g" /etc/php7/php-fpm.conf \
    && sed -i "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" /etc/php7/php-fpm.d/www.conf \
    && sed -i "s|;*listen\s*=\s*/||g" /etc/php7/php-fpm.d/www.conf \
    && sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini \
    && sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini \
    && sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php7/php.ini \
    && sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini \
    && sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini \
    && sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php7/php.ini

RUN \
    echo -e "\nInstalling misc packages..." && \
    apk add --update \
    bash \
    vim

# Clear cache.
RUN \
    echo -e "\nCleaning up temporary files..." \
    && apk del tzdata \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*

# Set work directory.
WORKDIR /var/www

# Start apache service in foreground.
ENTRYPOINT ["/usr/sbin/php-fpm7", "-D", "FOREGROUND"]

# Open web ports.
EXPOSE 9000
