from tbradburyacromediacom/awsdocker:php7

# Install PhpRedis
RUN pecl install redis-3.1.6 \
  && docker-php-ext-enable redis

# Get us a newer version of drush
RUN rm -rf /usr/local/bin/drush \
 && wget --quiet https://github.com/drush-ops/drush/releases/download/8.3.0/drush.phar \
 && mv drush.phar /usr/local/bin/drush \
 && chmod +x /usr/local/bin/drush
