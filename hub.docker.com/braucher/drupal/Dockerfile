# Drupal

FROM braucher/php
MAINTAINER Jeff Braucher <jeff@braucher.net>

# Install Drush
RUN composer create-project drush/drush /opt/drush --no-dev && \
  chmod a+x /opt/drush/drush && \
  ln -s /opt/drush/drush /usr/local/bin/drush

COPY ./app* /
ENTRYPOINT ["/app"]
CMD ["start"]

