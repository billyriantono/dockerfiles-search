FROM alpine:edge

LABEL MAINTAINER="Filip Hanes <filip.hanes@unitedclassifieds.sk>"

ENV TIMEZONE Europe/Bratislava

RUN apk add --update \
        bash \
        curl \
        git \
        openssl \
        php7 \
        php7-bcmath \
        php7-bz2 \
        php7-curl \
        php7-ctype \
        php7-dom \
        php7-gettext \
        php7-gmp \
        php7-iconv \
        php7-imagick \
        php7-imap \
        php7-json \
        php7-mcrypt \
        php7-mbstring \
        php7-mysqli \
        php7-odbc \
        php7-openssl \
        php7-phar \
        php7-pdo \
        php7-pdo_dblib \
        php7-pdo_odbc \
        php7-pdo_mysql \
        php7-pdo_pgsql \
        php7-pdo_sqlite \
        php7-soap \
        php7-simplexml \
        php7-sqlite3 \
        php7-xmlreader \
        php7-xmlrpc \
        php7-zip \
        tzdata \
    && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer \
    && rm -rf /var/cache/apk/* \
    && mkdir /web

#Build: docker build -t composer
#Test: docker run -v ~/ws/bazar:/web/bazar composer "cd /web/bazar && composer install"
