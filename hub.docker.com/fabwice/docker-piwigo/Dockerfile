# Image for Duniter releases on Linux.
#
# Building this image:
#   docker build . -t fabwice/docker-piwigo
# https://piwigo.org/doc/doku.php?id=user_documentation:use:features:new:htaccess_and_hotlink_in_2.4

FROM mathieuruellan/piwigo
MAINTAINER Fabwice <docker@fabwice.com>


ADD default.conf /etc/apache2/sites-enabled/000-default.conf
ADD .htaccess /var/www/.htaccess

RUN a2enmod rewrite
RUN /etc/init.d/apache2 restart

