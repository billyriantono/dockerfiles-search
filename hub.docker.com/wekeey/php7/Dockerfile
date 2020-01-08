FROM alpine:latest
MAINTAINER WeKeey <wekeey@mxw.me>

ENV TIMEZONE Asia/Shanghai
ENV PHP_MEMORY_LIMIT 512M
ENV MAX_UPLOAD 50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST 100M

RUN apk --update add tzdata \

    php7 \
    php7-intl \
    php7-openssl \
    php7-dba \
    php7-sqlite3 \
    php7-tokenizer \
    php7-phpdbg \
    php7-litespeed \
    php7-gmp \
    php7-pdo_mysql \
    php7-pcntl \
    php7-common \
    php7-oauth \
    php7-xsl \
    php7-fpm \
    php7-imagick \
    php7-mysqlnd \
    php7-enchant \
    php7-pspell \
    php7-redis \
    php7-snmp \
    php7-doc \
    php7-fileinfo \
    php7-mbstring \
    php7-dev \
    php7-xmlrpc \
    php7-embed \
    php7-xmlreader \
    php7-pdo_sqlite \
    php7-exif \
    php7-recode \
    php7-opcache \
    php7-ldap \
    php7-posix \
    php7-session \
    php7-gd \
    php7-gettext \
    php7-mailparse \
    php7-json \
    php7-xml \
    php7-iconv \
    php7-sysvshm \
    php7-curl \
    php7-shmop \
    php7-odbc \
    php7-phar \
    php7-pdo_pgsql \
    php7-imap \
    php7-pdo_dblib \
    php7-pgsql \
    php7-pdo_odbc \
    php7-xdebug \
    php7-zip \
    php7-cgi \
    php7-ctype \
    php7-amqp \
    php7-mcrypt \
    php7-wddx \
    php7-bcmath \
    php7-calendar \
    php7-tidy \
    php7-dom \
    php7-sockets \
    php7-zmq \
    php7-memcached \
    php7-soap \
    php7-apcu \
    php7-sysvmsg \
    php7-zlib \
    php7-imagick-dev \
    php7-ssh2 \
    php7-ftp \
    php7-sysvsem \
    php7-pdo \
    php7-bz2 \
    php7-mysqli \
    php7-simplexml \
    php7-xmlwriter \
    curl \
    curl-dev \
    postgresql-dev && \

    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    apk del tzdata && \

    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /bin/composer && \
    composer self-update && \

    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php7/php-fpm.conf && \
    sed -i -e "s/listen\s*=\s*127.0.0.1:9000/listen = 9000/g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;date.timezone =.*|date.timezone = ${TIMEZONE}|" /etc/php7/php.ini && \
    sed -i "s|memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|" /etc/php7/php.ini && \
    sed -i "s|upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|" /etc/php7/php.ini && \
    sed -i "s|max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|" /etc/php7/php.ini && \
    sed -i "s|post_max_size =.*|max_file_uploads = ${PHP_MAX_POST}|" /etc/php7/php.ini && \

    rm -rf /var/cache/apk/*

EXPOSE 9000

STOPSIGNAL SIGTERM

CMD ["php-fpm7"]
