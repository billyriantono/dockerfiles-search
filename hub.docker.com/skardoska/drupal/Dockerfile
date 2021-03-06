# from https://www.drupal.org/requirements/php#drupalversions
FROM php:7.0-apache

# install the PHP extensions we need - and vim for drush settings.php editing
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev vim \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
        && docker-php-ext-install gd mbstring opcache pdo pdo_mysql pdo_pgsql zip

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
                echo 'opcache.memory_consumption=128'; \
                echo 'opcache.interned_strings_buffer=8'; \
                echo 'opcache.max_accelerated_files=4000'; \
                echo 'opcache.revalidate_freq=60'; \
                echo 'opcache.fast_shutdown=1'; \
                echo 'opcache.enable_cli=1'; \
        } > /usr/local/etc/php/conf.d/opcache-recommended.ini

# https://www.drupal.org/node/3060/release
ENV DRUPAL_VERSION 8.0.6
ENV DRUPAL_MD5 952c14d46f0b02bcb29de5c3349c19ee

#Pull down drupal source
RUN curl -fSL "http://ftp.drupal.org/files/projects/drupal-${DRUPAL_VERSION}.tar.gz" -o /usr/src/drupal-${DRUPAL_VERSION}.tar.gz

#Pull down drush
RUN curl -fSL "http://files.drush.org/drush.phar" -o /usr/local/bin/drush

#Make drush executable
RUN chmod +x /usr/local/bin/drush

#Move in the entrypoint script
COPY drupal_entrypoint.sh /usr/local/sbin/entrypoint.sh

#Define data volumes
VOLUME ["/var/www/html"]


#Set the entrypoint
ENTRYPOINT ["entrypoint.sh"]
CMD ["apache2-foreground"]
