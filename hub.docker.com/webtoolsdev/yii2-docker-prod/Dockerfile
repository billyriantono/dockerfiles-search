FROM php:7.3-fpm-alpine
LABEL maintainer="bruce <bruce@webtools.co.nz>"

ENV ENABLE_CRON_JOB=${ENABLE_CRON_JOB:-true}
ENV ENABLE_PHPFPM=${ENABLE_PHPFPM:-true}
ENV ENABLE_YII2_QUEUE=${ENABLE_YII2_QUEUE:-false}
ENV YII2_QUEUE_WORKERS=${YII2_QUEUE_WORKERS:-4}

WORKDIR /app

COPY config /tmp/config

# Install system packages
RUN apk update && \
    apk add --no-cache \
        bash \
        git \
        freetds \
        freetype \
        icu \
        libintl \
        libldap \
        libjpeg \
        libmcrypt \
        libpng \
        libzip \
        libpq \
        libwebp \
        libmemcached \
        supervisor \
        curl \
        imagemagick \
        composer \
        $PHPIZE_DEPS && \
    apk add --no-cache --virtual build-dependencies \
        curl-dev \
        freetds-dev \
        freetype-dev \
        gettext-dev \
        icu-dev \
        jpeg-dev \
        libmcrypt-dev \
        libpng-dev \
        libmemcached-dev \
        libwebp-dev \
        libxml2-dev \
        libzip-dev \
        openldap-dev \
        postgresql-dev \
        imagemagick-dev \
        zlib-dev \
        autoconf \
        build-base && \
# Install PHP extensions
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure ldap --with-libdir=lib/ && \
    docker-php-ext-configure pdo_dblib --with-libdir=lib/ && \
    docker-php-ext-install \
        bcmath \
        curl \
        gettext \
        gd \
        exif \
        iconv \
        intl \
        ldap \
        mbstring \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        pdo_dblib \
        soap \
        sockets \
        zip && \
# Install PECL extensions
    pecl install imagick memcached && \
    docker-php-ext-enable imagick memcached && \
    apk del build-dependencies && \
    pecl install pcov && \
    docker-php-ext-enable pcov && \
# Download trusted certs
    mkdir -p /etc/ssl/certs && update-ca-certificates && \
# Copy php configuration
    cp /tmp/config/php.ini /usr/local/etc/php/php.ini && \
# Copy supervisor config
    mkdir /etc/supervisor.d && \
    cp /tmp/config/supervisord.conf /etc/supervisord.conf && \
    cp -r /tmp/config/supervisor.d /etc && \
# Copy cron job
    cp /tmp/config/crontab /etc/crontabs/root && \
    cp /tmp/config/entrypoint.sh /entrypoint.sh && \
    rm -rf /tmp/config && \
    chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]

