# Drush Docker Container
FROM zalari/composer
MAINTAINER Christian Ulbrich <christian.ulbrich@zalari.de>

# Install latest HEAD Drush using Composer
RUN composer global require drush/drush:dev-master

# Setup the symlink
RUN ln -sf $COMPOSER_HOME/vendor/bin/drush.php /usr/local/bin/drush

# Display which version of Drush was installed
RUN drush --version

# Update the entry point of the application
ENTRYPOINT ["drush"]
