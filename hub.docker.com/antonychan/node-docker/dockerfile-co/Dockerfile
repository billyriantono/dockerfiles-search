FROM php:5.4-fpm

# --------------
# Version 1
# --------------
RUN apt-get update; \
  apt-get -y install wget vim curl mysql-client; \
  apt-get -y install libmcrypt-dev libpng12-dev libfreetype6-dev libjpeg62-turbo-dev; \
  docker-php-ext-install mcrypt; \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \
  cd ~; \
  wget https://raw.githubusercontent.com/andytruong/snippets/master/Bash/.profile -O .bash_profile; \
  wget https://github.com/drush-ops/drush/archive/6.x.tar.gz -O /tmp/drush-6.x.tar.gz > /dev/null; \
  tar zxf /tmp/drush-6.x.tar.gz -C /tmp; \
  chmod a+x /tmp/drush-6.x/drush; \
  mv /tmp/drush-6.x/ /usr/local/lib/drush; \
  ln -s /usr/local/lib/drush/drush /usr/local/bin/drush; \
  curl -sS https://getcomposer.org/installer | php; \
  chmod a+x composer.phar; \
  mv composer.phar /usr/local/bin/composer;

CMD ["php-fpm -D"]
