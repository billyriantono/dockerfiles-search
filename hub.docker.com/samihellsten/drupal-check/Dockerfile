FROM wodby/drupal
LABEL maintainer="dropa@dropa.net"

RUN composer global require mglaman/drupal-check

WORKDIR /var/www/html

CMD ["drupal-check"]
