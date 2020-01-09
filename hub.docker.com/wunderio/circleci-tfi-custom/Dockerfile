FROM circleci/php:7.2-cli-node

# Add composer binary paths to global paths.
ENV PATH="/home/circleci/.composer/vendor/bin:${PATH}"

# Install drush, prestissimo and coder.
RUN composer global require drush/drush-launcher hirak/prestissimo drupal/coder \
  && phpcs --config-set installed_paths ~/.composer/vendor/drupal/coder/coder_sniffer \
  && composer clearcache

# Add custom php config. Increase memory to 256M
COPY conf/php/memory.ini /usr/local/etc/php/conf.d/memory.ini

# Install commonly used tools and libraries
RUN sudo apt-get update && sudo apt-get install -y libpng-dev default-mysql-client imagemagick

# Install mysql and zip php extensions
RUN sudo docker-php-ext-install pdo_mysql zip

# Install dockerize
RUN export DOCKERIZE_VERSION="v0.3.0" && sudo wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && sudo rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
