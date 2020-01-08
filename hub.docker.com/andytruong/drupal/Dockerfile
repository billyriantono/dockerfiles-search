# ---------------------
# mkdir drupal
# cd drupal
# wget https://gist.githubusercontent.com/andytruong/3f39b6cad443e17d2e96/raw/Dockerfile
# docker build -t at_drupal .
# docker run -t -i at_drupal /bin/bash

FROM    php:5.4-apache
COPY    ./drupal.make /var/www/drupal.make
WORKDIR /var/www/html/

# ---------------------
# Install required libs
# ---------------------
RUN apt-get update > /dev/null
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libmcrypt-dev libpng12-dev libfreetype6-dev libjpeg62-turbo-dev
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget curl vim git sqlite3 mysql-client php5-memcache
RUN DEBIAN_FRONTEND=noninteractive apt-get autoclean
RUN docker-php-ext-install mcrypt > /dev/null
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/
RUN docker-php-ext-install gd

# ---------------------
# Install Drush
# ---------------------
RUN wget https://github.com/drush-ops/drush/archive/6.x.tar.gz -O /tmp/drush-6.x.tar.gz > /dev/null
RUN tar zxf /tmp/drush-6.x.tar.gz -C /tmp
RUN chmod a+x /tmp/drush-6.x/drush
RUN mv /tmp/drush-6.x/ /usr/local/lib/drush
RUN ln -s /usr/local/lib/drush/drush /usr/local/bin/drush

# ---------------------
# Install composer
# ---------------------
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod a+x composer.phar
RUN mv composer.phar /usr/local/bin/composer

# ---------------------
# Make Drupal code base
# ---------------------
RUN  rm -rf /var/www/html && drush make /var/www/drupal.make /var/www/html
COPY ./local.settings.php /var/www/html/sites/default/local.settings.php

EXPOSE 80
CMD ["/bin/bash", "/start.sh"]
