FROM lxmltj/php7
MAINTAINER Ximing LU <lxmltj@gmail.com>

# Install extra utils
# Add drush
# Set the Drush version.
ENV DRUSH_VERSION 8.3.0

# Install Drush 8 with the phar file.
RUN curl -fsSL -o /usr/local/bin/drush "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" && \
    chmod +x /usr/local/bin/drush

# Add drupal console
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
    && php -r "readfile('https://drupalconsole.com/installer');" > drupal.phar \
    && mv drupal.phar /usr/local/bin/drupal \
    && chmod +x /usr/local/bin/drupal \
    && drupal init --override
    
