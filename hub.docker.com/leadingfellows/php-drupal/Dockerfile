FROM wodby/php:7.3
USER root
RUN  set -ex && \
	 curl https://drupalconsole.com/installer -L -o drupal.phar && \
	 curl -o drush.phar -L https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drushconsole && \
	 mv drupal.phar /usr/local/bin/drupal && \
     mv drush.phar /usr/local/bin/drush && \
	 chown www-data:www-data /usr/local/bin/drupal /usr/local/bin/drush && \
	 chmod +x /usr/local/bin/drupal /usr/local/bin/drush

USER www-data
RUN   composer global init --stability dev&& \
      composer global config prefer-stable true && \
      composer global require -vvv drush/drush drupal/console
USER wodby
