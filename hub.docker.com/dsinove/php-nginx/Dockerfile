FROM php:7.3-fpm-alpine

RUN apk update

RUN apk --no-cache add shadow \
    php7 php7-fpm php7-json php7-openssl php7-curl php7-phar php7-iconv php7-mbstring php7-dom php7-xmlwriter \
    php7-tokenizer php7-xml \
    nginx supervisor curl git openssh \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN useradd -m app -G `whoami`

RUN chown -R app /run \
  && chown -R app /var/lib/nginx \
  && chown -R app /var/tmp/nginx \
  && chown -R app /var/log/nginx

COPY docker/containers/web/nginx/etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY docker/containers/web/php/etc/php7/php-fpm.d/fpm-pool.conf /etc/php7/php-fpm.d/www.conf
COPY docker/containers/web/php/etc/php7/conf.d/php.ini /etc/php7/conf.d/zzz_custom.ini
COPY docker/containers/web/supervisor/etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

WORKDIR /var/www/html

EXPOSE 8080