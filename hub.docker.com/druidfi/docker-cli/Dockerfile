FROM php:7.2-cli-alpine

ENV ALPINE_VERSION=3.8 \
    COMPOSER_ALLOW_SUPERUSER=1

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    #
    # Install build dependencies
    #
    apk add --no-cache --virtual .build-deps \
        g++ \
        make \
        autoconf \
        yaml-dev \
        zlib-dev && \
    #
    # Install packages
    #
    apk add --no-cache \
        git \
        openssh \
        zip \
        unzip \
        yarn && \
    #
    # Configure PHP extensions
    #
    docker-php-ext-configure json && \
    docker-php-ext-configure mbstring && \
    docker-php-ext-configure zip && \
    #
    # Build and install PHP extensions
    #
    docker-php-ext-install \
        json \
        mbstring \
        opcache \
        zip && \
    #
    # Install MongoDB drivers
    #
    pecl install mongodb && docker-php-ext-enable mongodb && \
    docker-php-source delete && \
    #
    # Install Composer
    #
    curl -sS https://getcomposer.org/installer | php -- \
            --install-dir=/usr/local/bin \
            --filename=composer && \
            composer global require --optimize-autoloader "hirak/prestissimo" && \
            composer global dumpautoload --optimize && \
            composer clear-cache && \
    #
    # Remove build deps and caches
    #
    apk del .build-deps && \
    rm -rf /tmp/* && \
    rm -rf /usr/src/php.tar.* && \
    rm -rf /var/cache/apk/*

WORKDIR /app
