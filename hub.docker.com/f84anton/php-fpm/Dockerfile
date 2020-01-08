FROM f84anton/php-fpm:7.1

RUN docker-php-source extract \
  && pecl install xdebug \
  && docker-php-source delete \
  && rm -rf /tmp/pear \
  && docker-php-ext-enable xdebug

COPY xdebug.ini /usr/local/etc/php/conf.d/