FROM treillage/base:latest
LABEL maintainer="Meraj Sahebdar <itsdrewstiles@gmail.com>" \
    com.treillage.name="base-php" \
    com.treillage.vendor="treillage" \
    com.treillage.vcs-url="https://github.com/treillage/images" \
    com.treillage.version="1.0.0" \
    com.treillage.license="MIT"

ENV NGINX_CACHE_BACKGROUND_UPDATE="on" \
    NGINX_CACHE_DURATION="30s" \
    NGINX_CACHE_INACTIVE="1h" \
    NGINX_CACHE_KEY_STORAGE_SIZE="10m" \
    NGINX_CACHE_PATH="/var/cache/nginx" \
    NGINX_CACHE_SIZE="250m" \
    NGINX_FASTCGI_BUFFERS="8 8k" \
    NGINX_FASTCGI_BUFFER_SIZE="8k" \
    NGINX_FASTCGI_READ_TIMEOUT="120s" \
    NGINX_WORKER_CONNECTIONS=8000
ENV PHP_DISPLAY_ERRORS="Off" \
    PHP_DISPLAY_STARTUP_ERRORS="Off" \
    PHP_ERROR_REPORTING="E_ALL & ~E_DEPRECATED & ~E_STRICT" \
    PHP_FPM_PM_MAX_CHILDREN=10 \
    PHP_FPM_PM_MAX_REQUESTS=500 \
    PHP_FPM_PM_MAX_SPARE_SERVERS=3 \
    PHP_FPM_PM_MIN_SPARE_SERVERS=1 \
    PHP_FPM_PM_START_SERVERS=1 \
    PHP_MAX_EXECUTION_TIME=120 \
    PHP_MAX_INPUT_TIME=300 \
    PHP_MAX_INPUT_VARS=1000 \
    PHP_MEMORY_LIMIT="96M" \
    PHP_OPCACHE_ENABLE=1 \
    PHP_OPCACHE_ENABLE_CLI=1 \
    PHP_OPCACHE_FAST_SHUTDOWN=1 \
    PHP_OPCACHE_INTERNED_STRINGS_BUFFER=8 \
    PHP_OPCACHE_MAX_ACCELERATED_FILES=4000 \
    PHP_OPCACHE_MEMORY_CONSUMPTION=120 \
    PHP_OPCACHE_REVALIDATE_FREQ=60 \
    PHP_OUTPUT_BUFFERING="Off" \
    PHP_POST_MAX_SIZE="25M" \
    PHP_SENDMAIL_PATH="/usr/sbin/ssmtp -t" \
    PHP_SESSION_COOKIE_HTTPONLY="On" \
    PHP_SESSION_COOKIE_SECURE="Off" \
    PHP_SESSION_SAVE_PATH="/tmp" \
    PHP_TIMEZONE="UTC" \
    PHP_TRACK_ERRORS="Off" \
    PHP_UPLOAD_MAX_FILESIZE="25M"
ENV WEB_ROOT="/home/app/www" \
    WEB_USER="app" \
    WEB_GROUP="app"


COPY add-on/ /opt/

RUN set -x \
    # Setup php
    && apk add --no-cache --upgrade \
        # Install php
        php7-fpm \
        php7-json \
        php7-intl \
        php7-curl \
        php7-mysqli \
        php7-mysqlnd \
        php7-pdo_mysql \
        php7-pdo_pgsql \
        php7-pdo_sqlite \
        php7-mcrypt \
        php7-gd \
        php7-imagick \
        php7-imap \
        php7-bcmath \
        php7-soap \
        php7-sqlite3 \
        php7-bz2 \
        php7-calendar \
        php7-ctype \
        php7-pcntl \
        php7-pgsql \
        php7-posix \
        php7-sockets \
        php7-sysvmsg \
        php7-sysvsem \
        php7-sysvshm \
        php7-xmlreader \
        php7-exif \
        php7-ftp \
        php7-gettext \
        php7-iconv \
        php7-zip \
        php7-zlib \
        php7-shmop \
        php7-wddx \
        php7-xmlrpc \
        php7-xsl \
        php7-ldap \
        php7-redis \
        php7-pear \
        php7-phar \
        php7-openssl \
        php7-session \
        php7-opcache \
        php7-mbstring \
        php7-iconv \
        php7-apcu \
        php7-fileinfo \
        php7-simplexml \
        php7-tokenizer \
        php7-xmlwriter \
        # Install nginx
        nginx \
    # Configure pecl & pear
    && pecl channel-update pecl.php.net \
    && pear channel-update pear.php.net \
    && pear upgrade-all \
    && pear config-set auto_discover 1 \
    # NOTE: https://github.com/webdevops/Dockerfile/issues/78
    && sed -i "s/ -n / /" $(which pecl) \
    # Install php-mongodb extension
    && apk add --no-cache --virtual .deps-php-mongodb openssl-dev pcre-dev php7-dev build-base autoconf \
    && pecl install mongodb \
    && apk del .deps-php-mongodb \
    && echo "extension=mongodb.so" > /etc/php7/conf.d/mongodb.ini \
    # Install PHP composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && image-build \
    && image-clean

EXPOSE 80
