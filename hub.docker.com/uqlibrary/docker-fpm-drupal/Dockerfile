FROM uqlibrary/docker-fpm56:5

RUN \
 wget http://files.drush.org/drush.phar && \
 php drush.phar core-status && \
 chmod +x drush.phar && \
 mv drush.phar /usr/local/bin/drush && \
 drush init

EXPOSE 9000
