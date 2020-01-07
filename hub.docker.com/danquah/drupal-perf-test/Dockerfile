FROM drupal:7
RUN curl http://files.drush.org/drush.phar -o /usr/bin/drush && chmod a+x /usr/bin/drush

COPY perftest.sh /
VOLUME [/storage]
WORKDIR /
CMD [ "/perftest.sh" ]
