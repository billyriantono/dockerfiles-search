FROM php:alpine

ENV COMPOSER_HOME=/var/lib/composer \
    COMPOSER_CACHE_DIR=/var/cache/composer \
    COMPOSER_ALLOW_SUPERUSER=1

RUN apk add --no-cache git zlib-dev \
    && docker-php-ext-install zip mbstring

ENV COMPOSER_VERSION 1.4.2
COPY docker/composer.sh ./composer.sh
RUN ./composer.sh --install-dir=/usr/local/bin --filename=composer \
    && composer global require "hirak/prestissimo:^0.3" \
    && rm -rf composer.sh

ENTRYPOINT ["composer"]
CMD ["--help"]
