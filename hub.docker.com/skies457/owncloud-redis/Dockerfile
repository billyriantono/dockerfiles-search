FROM php:7.2.19 AS build
WORKDIR /
RUN curl -sSL https://pecl.php.net/get/redis-5.0.0.tgz -o redis-5.0.0.tgz \
 && tar -xvf redis-5.0.0.tgz \
 && cd redis-5.0.0 \
 && phpize \
 && ./configure \
 && make

FROM bitnami/owncloud
COPY --from=build /redis-5.0.0/modules/redis.so /opt/bitnami/php/lib/php/extensions/
RUN echo 'extension=redis.so' >> /opt/bitnami/php/etc/php.ini

