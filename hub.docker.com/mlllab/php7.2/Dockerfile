FROM alpine:3.8
LABEL maintainer="MLL"

ENV PHP_MAX_EXECUTION_TIME=240
ENV PHP_MEMORY_LIMIT=128M
ENV PHP_MAX_INPUT_VARS=4096

# ensure www-data user exists
RUN set -x \
    && addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data

WORKDIR /var/www

EXPOSE 9000

CMD ["php-fpm7", "-F"]

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk --update --no-cache add \
        php7 \
        php7-fpm \
    && rm -rf /var/cache/apk/*

COPY content /
