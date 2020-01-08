#build php72nginx
FROM ubuntu:18.10

ENV LC_ALL=C.UTF-8 TZ=Europe/Moscow DEBIAN_FRONTEND=noninteractive

RUN set -x\
  && apt update -qq\
  && apt install software-properties-common curl -y\
  && apt install -y --auto-remove php7.2-fpm \
  && apt install -y --auto-remove php7.2 \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*

VOLUME /run/php

RUN set -x\
  && apt update -qq \
  && apt install -y --auto-remove\
      php7.2-geoip\
      php7.2-mongodb\
      php7.2-bcmath\
      php7.2-bz2\
      php7.2-curl\
      php7.2-dba\
      php7.2-gd\
      php7.2-imap\
      php7.2-intl\
      php7.2-ldap\
      php7.2-mbstring\
      php7.2-imagick\
      php7.2-mysql\
      php7.2-pgsql\
      php7.2-snmp\
      php7.2-soap\
      php7.2-xml\
      php7.2-xmlrpc\
      php7.2-zip\
      php7.2-memcached\
      pkg-php-tools\
  && curl -skS https://getcomposer.org/installer | php\
  && mv composer.phar /usr/local/bin/composer\
  && chown www-data:www-data /run/php \
  && mkdir /var/log/php-fpm \
  && chown -R www-data:www-data /var/log/php-fpm \
  && sed -ie 's/\/var\/log\/php7.2-fpm.log/\/var\/log\/php-fpm\/php7.2-fpm.log/g' /etc/php/7.2/fpm/php-fpm.conf \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*

COPY data/php/fpm/php.ini /etc/php/7.2/fpm/php.ini
COPY data/php/fpm/www.conf /etc/php/7.2/fpm/pool.d/www.conf
COPY data/php/cli/php.ini /etc/php/7.2/cli/php.ini

CMD ["/usr/sbin/php-fpm7.2", "--nodaemonize", "--fpm-config", "/etc/php/7.2/fpm/php-fpm.conf"]
