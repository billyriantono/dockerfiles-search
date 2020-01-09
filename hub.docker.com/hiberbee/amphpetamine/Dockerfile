FROM php:7.4-rc-alpine
LABEL maintainer="vlad@hiberbee.com"
LABEL description="A Docker image based on Alpine Linux for php & RoadRunner application server. Includes Redis, APCu & Memcached with IGBinary extension, PHP DataStructures & UUID"

ARG uuid_version=1.0.3
ARG redis_version=5.0.2
ARG pthreads_version=3.2.0
ARG memcached_version=3.1.3
ARG igbinary_version=3.0.1
ARG apcu_version=5.1.17
ARG xdebug_version=2.8.0beta1
ARG timezone=Etc/UTC

ARG user=hiberbee
ARG src_path="/app"
ARG document_root="public"
ARG http_port=8000
# amqp apcu bcmath ds gd igbinary intl ldap mbstring memcached mongodb mysqli opcache pcntl pdo_mysql pdo_pgsql redis xdebug uuid
ARG php_enabled_ext="amqp apcu bcmath ds gd igbinary intl ldap mbstring memcached mongodb opcache pcntl pdo_mysql pdo_pgsql redis uuid"
ENV MEMCACHED_DEPS="zlib-dev libmemcached-dev cyrus-sasl-dev" COMPOSER_VERSION="${composer_version}" COMPOSER_HOME="/home/${user}/.composer"

RUN apk add --no-cache \
        build-base \
        freetype-dev \
        groff \
        icu-dev \
        libffi-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libmemcached-libs \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libxpm-dev \
        libzip-dev \
        mariadb-dev \
        nano \
        oniguruma-dev \
        openldap-dev \
        openssh \
        pcre-dev \
        postgresql-dev \
        python \
        rabbitmq-c \
        rabbitmq-c-dev \
        ${MEMCACHED_DEPS} \
        ${PHPIZE_DEPS} && \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-gd \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-webp-dir=/usr/include/ \
        --with-xpm-dir=/usr/include/ \
        --enable-gd-native-ttf=/usr/include/ && \
        NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} \
        bcmath \
        gd \
        intl \
        ldap \
        mbstring \
        mysqli \
        opcache \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        soap \
        sockets \
        zip && \
    wget https://s3.amazonaws.com/aws-cli/awscli-bundle.zip && \
    unzip awscli-bundle.zip && \
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws && \
    mkdir /tmp/libuuid && cd /tmp/libuuid && \
    wget -O- https://sourceforge.net/projects/libuuid/files/libuuid-${uuid_version}.tar.gz | tar xz && \
    cd "libuuid-${uuid_version}" && \
        ./configure && \
        make && \
        make install && \
    docker-php-source extract && \
    pecl install -o -f \
        amqp \
        ds \
        mongodb \
        uuid \
        xdebug-${xdebug_version} && \
    mkdir -p /usr/src/php/ext/apcu && curl -fsSL https://github.com/krakjoe/apcu/archive/v${apcu_version}.tar.gz | tar xvz -C /usr/src/php/ext/apcu --strip 1 && \
    docker-php-ext-install apcu && \
    mkdir -p /usr/src/php/ext/igbinary && curl -fsSL https://github.com/igbinary/igbinary/archive/${igbinary_version}.tar.gz | tar xvz -C /usr/src/php/ext/igbinary --strip 1 &&\
    docker-php-ext-install igbinary &&\
    mkdir -p /usr/src/php/ext/redis && curl -fsSL https://github.com/phpredis/phpredis/archive/${redis_version}.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 && \
    docker-php-ext-configure redis --enable-redis-igbinary && \
    docker-php-ext-install redis && \
    mkdir -p /usr/src/php/ext/memcached && curl -fsSL https://github.com/php-memcached-dev/php-memcached/archive/v${memcached_version}.tar.gz | tar xvz -C /usr/src/php/ext/memcached --strip 1 && \
    docker-php-ext-configure memcached --enable-memcached-igbinary && \
    docker-php-ext-install memcached && \
    docker-php-ext-enable ${php_enabled_ext} && \
    pecl clear-cache && \
    docker-php-source delete && \
    apk del --no-cache \
        build-base \
        libffi-dev \
        libmcrypt-dev \
        libx11-dev \
        rabbitmq-c-dev \
        pcre-dev \
        ${MEMCACHED_DEPS} \
        ${PHPIZE_DEPS} && \
    rm -rf \
        /usr/share/php7/* \
        /tmp/* \
        /usr/src/*

COPY conf.d/* /usr/local/etc/php/conf.d/
RUN ln -snf /usr/share/zoneinfo/${timezone} /etc/localtime
COPY --from=composer /usr/bin/composer /usr/local/bin/composer
COPY --from=512k/roadrunner /usr/bin/rr /usr/local/bin/rr

ENV SHELL=/bin/sh TERM=xterm-256color PATH="${PATH}:/usr/local/aws/bin:${HOME}/bin:${HOME}/.composer/vendor/bin:${src_path}/vendor/bin"
RUN composer global require hirak/prestissimo  --no-plugins --no-scripts
WORKDIR ${src_path}
EXPOSE ${http_port}

CMD ["rr", "-v", "-d", "serve"]
