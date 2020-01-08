FROM teknakat/npf:latest

ENV ENVIRONMENT prod

RUN apk add --no-cache \
  mysql-client \
  rsync openssh-client

# Install drush with composer
RUN composer global require drush/drush:8.* \
  && ln -s ~/.composer/vendor/bin/drush /usr/local/bin/drush \
  && drush core-status -y

ENV MEMCACHED_DEPS zlib-dev libmemcached-dev cyrus-sasl-dev
RUN apk add --no-cache --update libmemcached-libs zlib
RUN set -xe \
    && apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
    && apk add --no-cache --update --virtual .memcached-deps $MEMCACHED_DEPS \
    && pecl install memcached \
    && echo "extension=memcached.so" > /usr/local/etc/php/conf.d/20_memcached.ini \
    && rm -rf /usr/share/php7 \
    && rm -rf /tmp/* \
    && apk del .memcached-deps .phpize-deps

COPY conf/nginx /var/www/html/conf/nginx
COPY conf/drupal /var/www/html/conf/drupal
COPY conf/crontab /var/www/html/conf/crontab
COPY scripts /var/www/html/scripts
COPY src/web /var/www/html/src/web

# Set directory permissions
RUN chown -R nobody:nobody /var/www/html/src/web
