FROM casit/php:version2.0

# Install a current version of Drush
ENV DRUSH_VERSION 8.1.18
RUN curl -L --silent https://github.com/drush-ops/drush/releases/download/${DRUSH_VERSION}/drush.phar \
  > /usr/local/bin/drush && chmod +x /usr/local/bin/drush

# Used by drush to bootstrap drupal
RUN apt-get update && apt-get install -y mysql-client

# Install LDAP
RUN apt-get install -y libldap2-dev
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu
RUN docker-php-ext-install ldap

# For Drupal 8
RUN docker-php-ext-install opcache
COPY opcache-recommended.ini /usr/local/etc/php/conf.d
 
