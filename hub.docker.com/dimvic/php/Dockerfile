FROM php:7.3-fpm-alpine

# https://github.com/yiisoft/yii2-docker

ENV TERM=linux \
#    PATH=/app:/app/vendor/bin:/root/.composer/vendor/bin:$PATH \
#    PHP_ENABLE_XDEBUG=0 \
#    COMPOSER_ALLOW_SUPERUSER=1
    VERSION_PRESTISSIMO_PLUGIN=^0.3.7

ARG DOCKER_VERSION=19.03.3

ARG EXT_IMAGICK_VERSION=3.4.3
ARG EXT_TIDY_VERSION=5.6.0
ARG EXT_SWOOLE_VERSION=4.4.8

RUN    apk add su-exec

# add the docker client
RUN    curl -fsSLO "https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz" \
    && tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/local/bin \
    && rm -f docker-${DOCKER_VERSION}.tgz

# deps
RUN    set -x \
    && apk add --virtual .phpize-deps \
         autoconf file gcc g++ libtool libc-dev make cmake pkgconf re2c \
         freetype-dev libpng-dev libjpeg-turbo-dev libxml2-dev imagemagick-dev \
         openssl openssl-dev libmcrypt-dev \
         gettext gettext-libs gettext-dev \
         freetds-dev bzip2-dev \
         icu-dev curl-dev pcre-dev postgresql-dev \
    && apk add --virtual .runtime-freetds freetds \
    && apk add --virtual .runtime-gd      freetype libjpeg-turbo libpng \
    && apk add --virtual .runtime-gettext libintl \
    && apk add --virtual .runtime-imagick imagemagick \
    && apk add --virtual .runtime-intl    libintl \
    && apk add --virtual .runtime-mcrypt  libmcrypt libltdl \
    && apk add --virtual .runtime-pcre    pcre \
    && apk add --virtual .runtime-zip     libzip-dev \
    && apk add --virtual .runtime-xml     libxml2 \
    && apk add --virtual .yii2            icu

RUN    apk add bash bash-completion git curl \
    && apk add nodejs

# swoole
RUN    docker-php-ext-install sockets
RUN    mkdir /root/swoole && cd /root/swoole \
    && curl -fsSLO "https://github.com/swoole/swoole-src/archive/v${EXT_SWOOLE_VERSION}.tar.gz" \
    && tar -zxf "v${EXT_SWOOLE_VERSION}.tar.gz" \
    && cd "swoole-src-${EXT_SWOOLE_VERSION}" && phpize \
    && ./configure --enable-sockets --enable-openssl --enable-http2 --enable-mysqlnd \
    && make && make install \
    && rm -rf /root/swoole \
#    && echo "extension=sockets.so" >> /usr/local/etc/php/php.ini \
    && echo "extension=swoole.so" >> /usr/local/etc/php/conf.d/docker-php-ext-swoole.ini

# tidy
RUN    mkdir /root/tidy && cd /root/tidy \
    && curl -fsSLO "https://github.com/htacg/tidy-html5/archive/${EXT_TIDY_VERSION}.tar.gz" \
    && tar -zxf "${EXT_TIDY_VERSION}.tar.gz" \
    && cd "tidy-html5-${EXT_TIDY_VERSION}/build/cmake" && cmake ../.. -DCMAKE_BUILD_TYPE=Release \
    && make install \
    && rm -rf /root/tidy \
    && docker-php-ext-install tidy

# imagick
RUN    pecl install imagick-${EXT_IMAGICK_VERSION} \
    && docker-php-ext-enable imagick

# gd
RUN docker-php-ext-configure gd \
       --with-gd \
       --with-freetype-dir=/usr/include/ \
       --with-png-dir=/usr/include/ \
       --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# "standard"
RUN    docker-php-ext-install bz2 \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install ctype \
    && docker-php-ext-install curl \
    && docker-php-ext-install exif \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install gettext \
#    && docker-php-ext-install mcrypt \
#    && docker-php-ext-install mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install opcache \
    && docker-php-ext-install pdo_dblib \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install shmop \
    && docker-php-ext-install soap \
    && docker-php-ext-install sysvmsg \
    && docker-php-ext-install wddx \
#    && docker-php-ext-install xsl \
    && docker-php-ext-install zip

# Install composer
RUN    curl -sS https://getcomposer.org/installer | php -- \
       --filename=composer \
       --install-dir=/usr/local/bin \
    && composer clear-cache

# Install composer plugins
RUN    composer global require --optimize-autoloader "hirak/prestissimo:${VERSION_PRESTISSIMO_PLUGIN}" \
    && composer global dumpautoload --optimize \
    && composer clear-cache

# cleanup
RUN    apk del .phpize-deps \
    && rm -rf /tmp/* /var/cache/apk/*
