FROM daspanel/alpine-base
MAINTAINER Abner G Jacobsen - http://daspanel.com <admin@daspanel.com>

# Set default env variables
ENV \
    # Stop container initialization if error occurs in cont-init.d, fix-attrs.d script's
    S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \

    # Timezone
    TZ="UTC" 

# PHP modules to install
ARG PHP_MODULES="php5-ctype php5-curl php5-dom php5-gd php5-iconv php5-intl \
    php5-json php5-mcrypt php5-memcache php5-mysql php5-mysqli php5-openssl \
    php5-pdo php5-pdo_mysql php5-pdo_pgsql php5-pdo_sqlite php5-pear \
    php5-pgsql php5-phar php5-sqlite3 php5-xml php5-zip php5-zlib \
    php5-pcntl php5-ftp php5-gettext php5-imap"

RUN apk update && \
    apk --update --no-cache add --virtual build_deps curl && \
    apk add --no-cache --update php5-fpm php5-cli $PHP_MODULES && \
    curl -sS https://getcomposer.org/installer \
        | php -- --install-dir=/usr/bin --filename=composer && \
    apk del build_deps && \
    rm -rf \
        /var/cache/apk/* \
        /usr/local/* \
        /tmp/src \
        /tmp/*

# Inject files in container file system
COPY rootfs /

# Expose ports for the service
EXPOSE 9000

