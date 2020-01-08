FROM alpine:3.6
MAINTAINER Tommy Muehle <tommy.muehle@gmail.com>

RUN apk --update --progress --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community add \
    curl \
    tini \
    php7 \
    php7-dom \
    php7-ctype \
    php7-simplexml \
    php7-phar \
    php7-bz2 \
    php7-tokenizer \
    && curl -sL http://static.phpmd.org/php/latest/phpmd.phar -o /usr/bin/phpmd \
    && chmod +x /usr/bin/phpmd \
    && apk del curl \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

VOLUME /app
WORKDIR /app

ENTRYPOINT ["/sbin/tini", "--", "phpmd"]