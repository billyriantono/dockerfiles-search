FROM alpine:3.5

ENV PHP_TIMEZONE=UTC
ENV PHP_MEMORY_LIMIT=128M
ENV PHP_ERROR_REPORTING="E_ALL \& ~E_DEPRECATED \& ~E_STRICT"
ENV PHP_DISPLAY_ERRORS=off
ENV PHP_DISPLAY_STARTUP_ERRORS=off
ENV PHP_HTML_ERRORS=off
ENV PHP_UPLOAD_MAX_FILESIZE=2M
ENV PHP_MAX_FILE_UPLOADS=20
ENV PHP_POST_MAX_SIZE=8M

RUN \
    apk update && \
    apk upgrade && \
    \
    apk add --no-cache \
        \
        # binaries
        curl \
        \
        # php 7
        php7 \
        php7-bcmath \
        php7-calendar \
        php7-ctype \
        php7-curl \
        php7-dom \
        php7-iconv \
        php7-intl \
        php7-json \
        php7-mbstring \
        php7-mcrypt \
        php7-mysqlnd \
        php7-opcache \
        php7-openssl \
        php7-pdo \
        php7-pdo_mysql \
        php7-pdo_sqlite \
        php7-phar \
        php7-posix \
        php7-session \
        php7-soap \
        php7-sqlite3 \
        php7-xml \
        php7-xmlrpc \
        php7-zip \
        php7-zlib \
    && \
    rm -frv /var/cache/apk/*

RUN \
    # /etc/php7/php.ini
    sed -i \
        -e "s|;*date.timezone =.*|date.timezone = ${PHP_TIMEZONE}|g" /etc/php7/php.ini \
        -e "s|memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|g" /etc/php7/php.ini \
        -e "s|error_reporting =.*|error_reporting = ${PHP_ERROR_REPORTING}|g" /etc/php7/php.ini \
        -e "s|display_errors =.*|display_errors = ${PHP_DISPLAY_ERRORS}|g" /etc/php7/php.ini \
        -e "s|display_startup_errors =.*|display_startup_errors = ${PHP_DISPLAY_STARTUP_ERRORS}|g" /etc/php7/php.ini \
        -e "s|html_errors =.*|html_errors = ${PHP_HTML_ERRORS}|g" /etc/php7/php.ini \
        -e "s|upload_max_filesize =.*|upload_max_filesize = ${PHP_UPLOAD_MAX_FILESIZE}|g" /etc/php7/php.ini \
        -e "s|max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOADS}|g" /etc/php7/php.ini \
        -e "s|post_max_size =.*|post_max_size = ${PHP_POST_MAX_SIZE}|g" /etc/php7/php.ini \
    && \
    ln -s /usr/bin/php7 /usr/bin/php

ENTRYPOINT ["php"]
CMD ["-a"]
