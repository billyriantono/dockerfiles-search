FROM php:5.6.30-apache

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint
COPY resize.php /var/www/html/
COPY attachments.php /var/www/html/
COPY phpinfo.php /var/www/html/

RUN docker-php-ext-install mysqli sockets && \
  a2enmod rewrite && \
  apt-get update && apt-get install -y libmemcached11 libmemcachedutil2 \
  libz-dev libmemcached-dev build-essential wget zlib1g-dev libfreetype6 \
  libfreetype6-dev libjpeg62-turbo libjpeg62-turbo-dev php5-curl && \
  docker-php-ext-install zip && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install gd

RUN echo display_errors = 0 > /usr/local/etc/php/php.ini && \
  apt-get remove -y build-essential libmemcached-dev libz-dev && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /tmp/pear && \
  chmod ugo+x /usr/local/bin/docker-entrypoint

ENTRYPOINT [ "docker-entrypoint" ]

