FROM hub.alterway.fr/composer:1.0.0-alpha10-5.6

RUN apt-get update && apt-get install -y  git  \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require drush/drush:6.5 --prefer-dist \
    && apt-get install -y mysql-client \
    && ln -sf /root/.composer/vendor/bin/drush.php /usr/local/bin/drush \
    && apt-get install -y unzip

WORKDIR /var/www

ENV PHP_php5enmod 'bcmath mbstring pcntl zip pdo_mysql opcache gd'
#COPY docker-entrypoint.sh /entrypoint.sh

#ENTRYPOINT ["/entrypoint.sh", "/usr/local/bin/drush"]


