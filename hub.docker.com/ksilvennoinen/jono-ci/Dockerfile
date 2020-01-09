FROM alpine:3.6
LABEL description "CircleCI test image for CakePHP apps"

RUN apk add --no-cache --update \
    php7 \
    php7-intl \
    php7-sqlite3 \
    php7-mbstring \
    php7-openssl \
    php7-simplexml \
    php7-pdo \
    php7-pdo_sqlite \
    php7-ctype \
    php7-session \
    php7-json \
    php7-phar \
    php7-zlib \
    php7-dom \
    php7-tokenizer \
    php7-xmlwriter \
    php7-xml \
    git \
    openssh \
    tar \
    gzip \
    ca-certificates \
    curl

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin --filename=composer
