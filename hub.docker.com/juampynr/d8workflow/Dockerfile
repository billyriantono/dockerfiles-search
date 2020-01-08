FROM drupal:8.6-apache

# Change docroot since we use Composer Drupal project.
RUN sed -ri -e 's!/var/www/html!/var/www/html/web!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www!/var/www/html/web!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Install composer and prestissimo.
COPY composer-installer.sh /tmp/composer-installer.sh
RUN apt-get update && \
    apt-get install -y wget unzip && \
    chmod +x /tmp/composer-installer.sh && \
    /tmp/composer-installer.sh && \
    mv composer.phar /usr/local/bin/composer && \
    composer global require hirak/prestissimo

# Install Drush launcher.
RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar && \
  chmod +x drush.phar && \
  mv drush.phar /usr/local/bin/drush

# Install XDebug.
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Install various useful commands.
RUN apt-get install -y \
  git \
  mysql-client \
  vim

EXPOSE 80
WORKDIR /var/www/html
