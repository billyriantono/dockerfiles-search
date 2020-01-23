FROM alpine:3.5

MAINTAINER Denis Arosquipa <darosquipa@dtransforma.com>

LABEL Description="A simple image Httpd, PHP with Phalcon using alpine Linux"

ARG ARG_TIMEZONE_DEFAULT
ARG ARG_DOCUMENT_ROOT
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so
ENV ENV_DOCUMENT_ROOT "${ARG_DOCUMENT_ROOT:-/apps}"
RUN apk --update add \
    tzdata \
    apache2 \
    php5-apache2 \
    curl \
    php5-json \
    php5-phar \
    php5-openssl \
    php5-mysql \
    php5-curl \
    php5-mcrypt \
    php5-pdo \
    php5-pdo_mysql \
    php5-ctype \
    php5-gd \
    php5-xml \
    php5-dom \
    php5-iconv \
    php5-phalcon \
    && echo 'extension=phalcon.so' > /etc/php5/conf.d/phalcon.ini \
    && rm -f /var/cache/apk/* \
    && mkdir /run/apache2 \
    && mkdir -p /opt/utils

EXPOSE 80

ADD start.sh /opt/utils/

RUN chmod +x /opt/utils/start.sh & \
    cp "/usr/share/zoneinfo/${ARG_TIMEZONE_DEFAULT:-America/Lima}" /etc/localtime & \
    apk del tzdata

WORKDIR $ENV_DOCUMENT_ROOT

ENTRYPOINT ["/opt/utils/start.sh"]
