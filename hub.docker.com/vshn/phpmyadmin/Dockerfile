FROM nazarpc/phpmyadmin:latest

# Privileged ports are not allowed on OpenShift, the container must not run
# with user root, and folders accessed by that user must belong to group root.
# See https://docs.openshift.com/container-platform/3.7/creating_images/guidelines.html#use-uid

RUN sed -i \
    -e 's/Listen 80/Listen 8080/' \
    -e 's/Listen 443/Listen 4443/' \
    /etc/apache2/ports.conf \
 && chgrp -R 0 /tmp /var/run/apache2 /var/www/html \
 && chmod -R g=u /tmp /var/run/apache2 /var/www/html
