FROM acfatah/php:7.0

RUN apk update && \
    apk upgrade && \
    \
    # install phpunit dependencies
    apk add --no-cache \
        libxml2 \
        php7-pcntl \
        php7-xdebug \
    && \
    # install phpunit
    composer global require \
        --no-interaction \
        --update-no-dev \
        \
        "phpunit/phpunit:^6.0" \
        "phpunit/php-invoker:^1.1" \
        "phpunit/dbunit:^3.0" \
    && \
    rm -rf /var/cache/apk/*

VOLUME ["/app"]
WORKDIR /app
ENTRYPOINT ["phpunit"]
CMD ["/app"]
