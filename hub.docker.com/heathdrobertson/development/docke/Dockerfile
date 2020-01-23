FROM alpine:3.8

RUN set -x \
    && apk add --no-cache \
        php7 \
        php7-ctype \
        php7-dom \
        php7-simplexml \
        php7-tokenizer \
        php7-phar \
    && wget -c http://static.phpmd.org/php/latest/phpmd.phar \
    && mv /phpmd.phar /usr/local/bin/phpmd \
    && chmod +x /usr/local/bin/phpmd \
    && mkdir -p /code

WORKDIR /code
VOLUME /code

ENTRYPOINT ["phpmd"]

