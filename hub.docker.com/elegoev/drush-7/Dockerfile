# Drush Docker Container
FROM composer/composer
MAINTAINER Urs Voegele

# Install Drush using Composer
RUN composer global require drush/drush:~7.1.0 --prefer-dist

# Setup the symlink
RUN ln -sf $COMPOSER_HOME/vendor/bin/drush.php /usr/local/bin/drush

# Display which version of Drush was installed
RUN drush --version

# Update the entry point of the application
ENTRYPOINT ["drush"]
