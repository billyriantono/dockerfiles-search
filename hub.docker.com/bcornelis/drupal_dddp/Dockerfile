FROM drupal:8.5-apache

WORKDIR /var/www/html

RUN apt-get update && apt-get install -y git

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --install-dir=/tmp \
  && php -r "unlink('composer-setup.php');" \
  && php /tmp/composer.phar require "drupal/address ~1.0" \
  && rm /tmp/composer.phar
