FROM jianhe/debian
MAINTAINER John Nie <80285394@qq.com>

# Install system packages
RUN apt-get install -y \
  git \
  unzip \
  wget

# Mysql server config
COPY 60-drupal.cnf /etc/mysql/conf.d/60-drupal.cnf
# Install Drupal
RUN rm -rf /var/www/html
RUN git clone -b 8.7.x git://git.drupal.org/project/drupal.git /var/www/html

WORKDIR /var/www/html
ENV COMPOSER_PROCESS_TIMEOUT 1200
RUN composer install

# Install Drupal modules
RUN composer require \
  drupal/r4032login \
  drupal/address \
  drupal/ajax_links_api \
  drupal/block_class \
  drupal/conditional_fields \
  drupal/console \
  drupal/custom_formatters \
  drush/drush \
  drupal/facets \
  drupal/features \
  drupal/field_formatter_class \
  drupal/field_group \
  drupal/inline_entity_form \
  drupal/memcache \
  drupal/pinyin \
  drupal/jsonapi \
  drupal/quicktabs \
  drupal/reference_table_formatter \
  drupal/relaxed \
  drupal/restui \
  drupal/rules \
  drupal/purge \
  drupal/search_api_solr \
  drupal/token \
  drupal/token_filter \
  drupal/views_slideshow \
  drupal/varnish_purge

RUN /etc/init.d/mysql start && \
  vendor/bin/drush si -y --account-pass=admin --db-url=mysql://root:@localhost/drupal

# Enable memcache modules
RUN /etc/init.d/mysql start && \
  vendor/bin/drupal moi -y \
    memcache
COPY settings.local.php sites/default/settings.local.php
RUN echo "include \$app_root . '/' . \$site_path . '/settings.local.php';" >> sites/default/settings.php

# Install varnish_purge
RUN /etc/init.d/mysql start && \
  vendor/bin/drupal moi -y \
    varnish_purger

# Finish
EXPOSE 80 3306 22 443
CMD exec supervisord -n
