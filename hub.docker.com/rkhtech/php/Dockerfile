# Dockerfile used to create an Apache/PHP environment for PHP sites
# includes awscli, and

FROM php:7-apache
MAINTAINER Randy Hommel <randy@hommel.name>

ENV TZ America/Los_Angeles

EXPOSE 80

WORKDIR /var/www/html
ENTRYPOINT /opt/entrypoint.sh

COPY opt /opt

RUN /opt/install/setup_root.sh
RUN /opt/install/update_os.sh
RUN /opt/install/configure_apache.sh
RUN /opt/install/configure_php.sh

RUN echo "<?php getinfo();" > /var/www/html/index.php
