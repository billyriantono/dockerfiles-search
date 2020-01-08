FROM gaxze/php-base:7.1

# Drupal Console
RUN curl -L https://github.com/hechoendrupal/drupal-console-launcher/releases/download/1.0.2/drupal.phar > drupal \
    && chmod +x drupal \
    && mv drupal /usr/local/bin/

# Install drush
RUN composer global config bin-dir /usr/local/bin \
  ; composer global require drush/drush
