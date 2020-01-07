FROM alpine:3.10

RUN set -x && addgroup -g 82 -S www-data && adduser -u 82 -D -S -G www-data www-data

RUN mkdir -p /var/www/ \
 && mkdir -p /var/run/php/ \
 && mkdir -p /var/log/php/ \
 && mkdir -p /var/log/app/ \
 && chown -R www-data:www-data /var/www/

RUN apk update && apk upgrade
RUN apk add nano mc bash-completion net-tools openssh-client chrpath curl wget rsync git unzip bzip2 g++ make su-exec openrc supervisor
RUN apk add php7-cli php7-json php7-openssl php7-iconv php7-ctype php7-soap php7-dom php7-bcmath php7-pgsql php7-mbstring php7-intl php7-curl php7-zip php7-gd php7-pear php7-redis php7-dev composer

RUN rm -rf /var/cache/apk/*

RUN pecl install mongodb && pecl clear-cache
RUN echo "extension=mongodb.so" > /etc/php7/conf.d/mongodb.ini

RUN mkdir /etc/supervisor && mkdir /etc/supervisor/conf.d/
RUN mkdir -p /var/log/supervisor
RUN chown -R www-data:www-data /var/log/supervisor

COPY supervisor/supervisord.conf /etc/supervisord.conf

RUN rc-update add supervisord default

WORKDIR /var/www/

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]