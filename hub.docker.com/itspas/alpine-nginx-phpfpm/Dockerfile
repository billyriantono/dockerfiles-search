FROM itspas/alpine:3.3

MAINTAINER Yenole "Netxy@vip.qq.com"

RUN apk --update add \
  nginx \
  php-fpm \
  php-pdo \
  php-json \
  php-openssl \
  php-mysql \
  php-pdo_mysql \
  php-mcrypt \
  php-sqlite3 \
  php-pdo_sqlite \
  php-ctype \
  php-zlib \
  php-curl \
  php-phar \
  php-xml \
  php-opcache \
  php-intl \
  php-bcmath \
  php-dom \
  php-xmlreader \
  php-gd \
  curl \
  supervisor \
  && rm -rf /var/cache/apk/*

ADD nginx.conf /etc/nginx/nginx.conf

VOLUME ["/usr/share/nginx/html", "/etc/nginx/sites-enabled"]

ADD nginx-phpfpm.ini /etc/supervisor.d/nginx-phpfpm.ini

EXPOSE 80 9000

CMD ["/usr/bin/supervisord"]
