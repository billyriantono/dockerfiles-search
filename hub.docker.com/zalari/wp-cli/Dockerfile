# wp-cli Docker Container
FROM zalari/composer
MAINTAINER David Enke <david.enke@zalari.de>

# Install latest HEAD wp-cli using Composer
RUN composer global require wp-cli/wp-cli:dev-master

# Symlink binary
RUN ln -sf $COMPOSER_HOME/vendor/bin/wp /usr/local/bin/wp

# Display which version of Drush was installed
RUN wp --allow-root --version

# Update the entry point of the application
ENTRYPOINT ["wp"]