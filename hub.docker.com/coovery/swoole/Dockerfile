FROM php:7.4

ENV SWOOLE_VERSION 4.4.12

RUN set -eux; \
        \
        apt-get update; \
        apt-get install -y --no-install-recommends \
                cron \
                git \
                procps \
                libfreetype6-dev \
                libjpeg-dev \
                libpng-dev \
                libssl-dev \
                libwebp-dev \
                libzip-dev \
                openssl \
                supervisor \
                unzip \
                zip \
        ; \
        rm -r /var/lib/apt/lists/*

RUN set -eux; \
        \
        docker-php-ext-configure gd \
                --with-freetype-dir=/usr/include/ \
                --with-jpeg-dir=/usr/include/ \
                --with-webp-dir=/usr/include/ \
        ; \
        docker-php-ext-install \
                gd \
                pcntl \
                pdo_mysql \
                sockets \
                zip \
        ;

RUN set -eux; \
        \
        curl -L https://github.com/swoole/swoole-src/archive/v$SWOOLE_VERSION.tar.gz -o php-swoole.tar.gz; \
        mkdir -p /usr/src/php-swoole; \
        tar -xzf php-swoole.tar.gz -C /usr/src/php-swoole --strip-components=1; \
        rm -rf php-swoole.tar.gz; \
        cd /usr/src/php-swoole; \
        phpize; \
        ./configure --enable-http2 --enable-mysqlnd --enable-openssl --enable-sockets; \
        make && make install; \
        docker-php-ext-enable swoole; \
        cd /

RUN set -eux; \
        \
        curl -L https://getcomposer.org/installer | php; \
        mv composer.phar /usr/local/bin/composer

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 8080

CMD ["supervisord", "-n"]
