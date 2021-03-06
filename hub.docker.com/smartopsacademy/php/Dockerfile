FROM php:7.3-fpm-alpine
MAINTAINER SmartOps Academy <docker@smartops.academy>

RUN apk update \
 && apk add zip unzip \
 && apk add --virtual .build-deps git bzip2-dev curl-dev freetype-dev gettext-dev libjpeg-turbo-dev libmcrypt-dev libpng-dev libxml2-dev libmcrypt-dev recode-dev libzip-dev \
 && docker-php-source extract \
 && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/phpredis \
 && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
 && docker-php-ext-install bcmath bz2 curl gd gettext mysqli opcache recode session soap zip phpredis \
 && phpdeps=$( \
      scanelf --needed --nobanner --recursive /usr/local/lib/php/extensions \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u \
      | xargs -r apk info --installed \
      | sort -u) \
 && apk add --virtual .phpexts-rundeps $phpdeps \
 && apk del .build-deps \
 && docker-php-source delete
RUN cd /usr/src \
 && curl -o /usr/src/ioncube_loaders_lin_x86-64.tar.gz https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
 && tar xzf ioncube_loaders_lin_x86-64.tar.gz \
 && cp ioncube/ioncube_loader_lin_7.3.so /usr/local/lib/php/extensions/no-debug-non-zts-*/ \
 && rm -rf ioncube* \
 && docker-php-ext-enable ioncube_loader_lin_7.3
RUN sed -i 's/www-data:x:82:82:/www-data:x:33:33:/' /etc/passwd \
 && sed -i 's/xfs:x:33:33:/xfs:x:82:82:/' /etc/passwd \
 && sed -i 's/www-data:x:82:www-data/www-data:x:33:www-data/' /etc/group \
 && sed -i 's/xfs:x:33:xfs/xfs:x:82:xfs/' /etc/group

COPY etc/ /usr/local/etc/

CMD ["/usr/local/sbin/php-fpm", "-F"]
