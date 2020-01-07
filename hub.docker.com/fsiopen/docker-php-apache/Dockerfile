FROM alpine:3.10
LABEL docker-php-apache.image=runtime

ENV LANG pl_PL.utf8
ENV LC_ALL pl_PL.UTF-8
ENV PROJECTROOT=/var/www
ENV APPROOT="$PROJECTROOT/application"
ENV DOCROOT="$APPROOT/web"

ENV PHP_PACKAGES php7 \
    php7-common \
    php7-apache2 \
    php7-json \
    php7-intl \
    php7-mbstring \
    php7-iconv \
    php7-opcache \
    php7-xml \
    php7-simplexml \
    php7-phar \
    php7-openssl \
    php7-sockets \
    php7-pdo \
    php7-pdo_sqlite \
    php7-pdo_mysql \
    php7-mysqlnd \
    php7-session \
    php7-soap \
    php7-curl \
    php7-gd \
    php7-zip \
    php7-ctype \
    php7-dom \
    php7-bcmath \
    php7-calendar \
    php7-xmlreader \
    php7-xmlwriter \
    php7-tokenizer \
    php7-exif \
    php7-fileinfo \
    php7-pecl-xdebug \
    argon2-libs \
    openssl \
    mailcap \
    curl \
    git

ENV HTTP_PACKAGES="apache2 apache2-ssl"
ENV DB_PACKAGES="mysql-client"
ENV NODE_PACKAGES="nodejs yarn"
ENV UTILS="shadow mc bash"
ENV PHP_INI_DIR /etc/php7
ENV HOST_UID 1000
ENV HOST_GID 1000

RUN set -xe && apk add --no-cache $UTILS && \
    addgroup -g $HOST_GID -S www-data && \
    adduser -u $HOST_UID -D -S -G www-data www-data -s /bin/bash && \
    apk add --no-cache $PHP_PACKAGES && \
    apk add --no-cache $DB_PACKAGES && \
    apk add --no-cache $NODE_PACKAGES && \
    mkdir -p "$DOCROOT"  && \
    mkdir -p /run/apache2 && \
    chown -R www-data:www-data "$PROJECTROOT" && \
    apk add --no-cache $HTTP_PACKAGES && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log && \
    sed -ri \
        -e 's!^#\s*ServerName.*!ServerName localhost!g' \
        -e 's!^User.*!User www-data!g' \
        -e 's!^Group.*!Group www-data!g' \
        -e 's!^#\s*(LoadModule rewrite_module modules/mod_rewrite.so)!\1!g' \
        /etc/apache2/httpd.conf;

COPY ./application-vhost.conf /etc/apache2/conf.d/application-vhost.conf
COPY ./php_custom.ini "$PHP_INI_DIR/conf.d/01_php_custom.ini"
COPY ./php_xdebug.ini "$PHP_INI_DIR/conf.d/01_php_xdebug.ini"

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin && \
    php -r "unlink('composer-setup.php');" && \
    chown www-data:www-data /usr/local/bin/composer.phar

EXPOSE 443 80

VOLUME $APPROOT
WORKDIR $APPROOT

CMD mkdir -p $DOCROOT && \
    usermod -u $HOST_UID www-data && \
    groupmod -g $HOST_GID www-data && \
    rm -f /run/apache2/httpd.pid && \
    httpd -DFOREGROUND
