
FROM llslim/docker-phpcli:latest

# install the drush launcher
RUN curl -OL https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar \
  && mv drush.phar /usr/local/bin/drush \
  && chmod +x /usr/local/bin/drush

# install the drupal console launcher
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  && mv drupal.phar /usr/local/bin/drupal \
  && chmod +x /usr/local/bin/drupal

ENTRYPOINT /bin/bash
