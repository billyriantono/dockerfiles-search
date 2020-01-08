FROM uqlibrary/docker-fpm56:1

RUN \
 pear channel-discover pear.drush.org  && \
 pear install drush/drush

EXPOSE 80