FROM alpine:3.7

# Alpine 3.7 is php 7.1

#RUN echo '@edge http://nl.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories && \
#echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
#echo '@community http://nl.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories && \


RUN  apk --update add \
        busybox-suid \
      	ca-certificates \
      	openssl \
        git \
        php7 \
        php7-bcmath \
        php7-bz2 \
        php7-ctype \
        php7-curl \
        php7-dom \
        php7-fpm \
        php7-gd \
        php7-iconv \
        php7-intl \
        php7-fileinfo \
        php7-json \
        php7-mbstring \
        php7-mcrypt \
        php7-mysqlnd \
        php7-opcache \
        php7-openssl \
        php7-pdo \
        php7-pdo_mysql \
        php7-phar \
        php7-posix \
        php7-redis \
        php7-session \
        php7-soap \
        php7-xml \
        php7-xmlwriter \
        php7-simplexml \
        php7-tokenizer \
        php7-zlib \
        php7-zip \
        php7-apcu \
        php7-memcached \
        mysql-client \
        optipng \
        jpegoptim \      
        shadow \
        ssmtp \
        curl \
        pdftk \
        && rm -rf /var/cache/apk/*

COPY php.ini /etc/php7/conf.d/50-setting.ini
COPY php-fpm.conf /etc/php7/php-fpm.conf
#RUN ln -s /usr/bin/php7 /usr/bin/php

# install composer
RUN wget https://getcomposer.org/download/1.6.5/composer.phar -O composer \
    && mv composer /usr/bin/composer \
    && chmod +x /usr/bin/composer \
    && composer self-update


# install Drush
ENV DRUSH_VERSION 8.1.7
RUN curl -L --silent https://github.com/drush-ops/drush/releases/download/${DRUSH_VERSION}/drush.phar \
  > /usr/local/bin/drush && chmod +x /usr/local/bin/drush


VOLUME /app
EXPOSE 9000

COPY docker-entrypoint.sh /var/entrypoint.sh
RUN chmod +x /var/entrypoint.sh

ENTRYPOINT ["/bin/sh", "/var/entrypoint.sh"]
