FROM martinussuherman/alpine-tz-ep

ENV LABEL_MAINTAINER="Martinus Suherman" \
    LABEL_VENDOR="martinussuherman" \
    LABEL_IMAGE_NAME="martinussuherman/alpine-tz-ep-php-fpm" \
    LABEL_URL="https://hub.docker.com/r/martinussuherman/alpine-tz-ep-php-fpm/" \
    LABEL_VCS_URL="https://github.com/martinussuherman/alpine-tz-ep-php-fpm" \
    LABEL_DESCRIPTION="Docker image for PHP-FPM, based on Alpine Linux." \
    LABEL_LICENSE="GPL-3.0" \
    # container/su-exec UID \
    EUID=9999 \
    # container/su-exec GID \
    EGID=9999 \
    # container/su-exec user name \
    EUSER=www-data \
    # container/su-exec group name \
    EGROUP=www-data \
    # container user home dir \
    EHOME=/etc/php7 \
    # additional directories to create + chown (space separated) \
    ECHOWNDIRS="/var/log/php-fpm" \
    # additional files to create + chown (space separated) \
    ECHOWNFILES="/var/log/php-fpm/access.log /var/log/php-fpm/error.log"

RUN apk add --no-cache \
    php7 \
    php7-fpm \
    # php7-amqp \
    # php7-apache2 \
    # php7-apcu \
    php7-bcmath \
    php7-bz2 \
    php7-calendar \
    php7-ctype \
    php7-curl \
    # php7-dba \
    php7-dom \
    php7-embed \
    # php7-enchant \
    # php7-exif \
    # php7-fileinfo \
    # php7-ftp \
    php7-gd \
    php7-gettext \
    php7-gmp \
    php7-iconv \
    php7-imagick \
    php7-imap \
    php7-intl \
    php7-json \
    # php7-ldap \
    # php7-litespeed \
    # php7-mailparse \
    php7-mbstring \
    # php7-mcrypt \
    # php7-memcached \
    php7-mysqli \
    php7-mysqlnd \
    # php7-oauth \
    # php7-odbc \
    php7-opcache \
    php7-openssl \
    # php7-pcntl \
    php7-pdo \
    # php7-pdo_dblib \
    php7-pdo_mysql \
    # php7-pdo_odbc \
    # php7-pdo_pgsql \
    php7-pdo_sqlite \
    # php7-pear \
    # php7-pear-auth_sasl \
    # php7-pear-auth_sasl2 \
    # php7-pear-mail_mime \
    # php7-pear-mdb2_driver_mysql \
    # php7-pear-mdb2_driver_pgsql \
    # php7-pear-net_idna2 \
    # php7-pear-net_smtp \
    # php7-pear-net_socket \
    php7-pgsql \
    php7-phar \
    # php7-phpdbg \
    # php7-posix \
    # php7-pspell \
    # php7-recode \
    php7-redis \
    php7-session \
    # php7-shmop \
    # php7-simplexml \
    # php7-snmp \
    php7-soap \
    php7-sockets \
    php7-sqlite3 \
    # php7-ssh2 \
    # php7-sysvmsg \
    # php7-sysvsem \
    # php7-sysvshm \
    # php7-tidy \
    # php7-tokenizer \
    # php7-wddx \
    # php7-xdebug \
    php7-xml \
    php7-xmlreader \
    # php7-xmlrpc \
    # php7-xmlwriter \
    # php7-xsl \
    php7-zip \
    # php7-zmq \
    && touch /var/log/php-fpm-access.log /var/log/php-fpm-error.log \
    && ln -sf /dev/stdout /var/log/php-fpm-access.log \
    && ln -sf /dev/stderr /var/log/php-fpm-error.log

ENTRYPOINT ["/entrypoint_exec.sh", "php-fpm7"]

ARG LABEL_VERSION="latest"
ARG LABEL_BUILD_DATE
ARG LABEL_VCS_REF

# Build-time metadata as defined at http://label-schema.org
LABEL maintainer=$LABEL_MAINTAINER \
      org.label-schema.build-date=$LABEL_BUILD_DATE \
      org.label-schema.description=$LABEL_DESCRIPTION \
      org.label-schema.name=$LABEL_IMAGE_NAME \
      org.label-schema.schema-version="1.0" \
      org.label-schema.url=$LABEL_URL \
      org.label-schema.license=$LABEL_LICENSE \
      org.label-schema.vcs-ref=$LABEL_VCS_REF \
      org.label-schema.vcs-url=$LABEL_VCS_URL \
      org.label-schema.vendor=$LABEL_VENDOR \
      org.label-schema.version=$LABEL_VERSION
