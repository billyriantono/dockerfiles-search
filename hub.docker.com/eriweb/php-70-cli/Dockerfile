FROM alpine:3.7

RUN apk update \
    && apk add php7 \
              php7-ctype \
               php7-curl \
               php7-dom \
               php7-gettext \
               php7-gmp \
               php7-iconv \
               php7-intl \
               php7-json \
               php7-mbstring \
               php7-mcrypt \
               php7-pcntl \
               php7-pdo \
               php7-pdo_mysql \
               php7-phar \
               php7-mysqli \
               php7-zip \
               php7-zlib \
               unzip \
               git \
               curl \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /var/cache/apk/*