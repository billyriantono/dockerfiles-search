FROM php:7.3-apache
  
RUN  apt-get update
RUN  apt-get -y install libicu-dev zlib1g-dev libzip-dev zip unzip git libpng-dev libxml2-dev default-mysql-server default-mysql-client
RUN  /usr/sbin/a2enmod rewrite
RUN  docker-php-ext-install intl pdo_mysql mysqli zip gd xml opcache
RUN  cd /home


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'baf1608c33254d00611ac1705c1d9958c817a1a33bce370c0595974b342601bd80b92a3f46067da89e3b06bff421f182') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

RUN composer global require laravel/installer
RUN PATH=$PATH:~/.composer/vendor/bin
RUN zip -r /tmp/apache.zip /etc/apache2
RUN cd /var/www/html

ADD zip.sh /tmp
RUN chmod 744 /tmp/zip.sh

RUN { \
  echo 'opcache.enable=1'; \
  echo 'opcache.optimization_level=0x7FFFBBFF' ; \
  echo 'opcache.revalidate_freq=0'; \
  echo 'opcache.validate_timestamps=1'; \
  echo 'opcache.memory_consumption=128'; \
  echo 'opcache.interned_strings_buffer=8'; \
  echo 'opcache.max_accelerated_files=4000'; \
  echo 'opcache.revalidate_freq=60'; \
  echo 'opcache.fast_shutdown=1'; \
} > /usr/local/etc/php/conf.d/overrides.ini


#CMD ["/tmp/zip.sh"]

CMD bash -c "/tmp/zip.sh && apache2-foreground"
