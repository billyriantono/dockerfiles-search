FROM alpine:3.10
LABEL Maintainer="24hoursmedia <info@24hoursmedia>" \
      Description="PHP-FPM 7.3 container started by supervisord"

RUN apk add --update --no-cache \
    coreutils \
    libmemcached-dev \
    php7-fpm \
    php7-apcu \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-gd \
    php7-exif \
    php7-mbstring \
    php7-iconv \
    php7-imagick \
    php7-json \
    php7-intl \
    php7-mcrypt \
    php7-fileinfo\
    php7-opcache \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-mysqli \
    php7-xml \
    php7-zlib \
    php7-phar \
    php7-tokenizer \
    php7-session \
    php7-simplexml \
    php7-xdebug \
    php7-zip \
    php7-xmlwriter \
    php7-memcached \
    php7-redis \
    php7-apcu \
    make \
    curl \
    supervisor

# fix work iconv library with alphine
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

# Configure PHP-FPM
COPY config/fpm-pool.conf /etc/php7/php-fpm.d/www.conf
COPY config/php.ini /etc/php7/conf.d/zzz_custom.ini

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Make sure files/folders needed by the processes are accessible when they run under the nobody user
RUN chown -R nobody.nobody /run
RUN mkdir -p /var/www/html && chown nobody:nobody /var/www/html
RUN mkdir -p /.composer/cache && chown -R nobody /.composer
VOLUME /.composer/cache

USER nobody

# install parallel downloads plugin for composer
RUN composer global require hirak/prestissimo


WORKDIR /var/www/html

COPY --chown=nobody src/ /var/www/html/

# Expose php-fpm port
EXPOSE 9000

# Let supervisord start php-fpm so we can add other processes later
COPY config/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY config/supervisor/php-fpm.ini /etc/supervisor/conf.d/php-fpm.ini

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]

# Configure a healthcheck to validate that everything is up&running
# HEALTHCHECK --timeout=10s CMD curl --silent --fail http://127.0.0.1:8080/fpm-ping