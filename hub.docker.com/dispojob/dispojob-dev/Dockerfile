FROM dispojob/dispojob-ci

RUN pecl update-channels \
 && pecl install xdebug-2.5.5 \
 && docker-php-ext-enable xdebug

COPY docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/