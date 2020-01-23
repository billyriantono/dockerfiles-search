FROM antoniorossi/magento_php54
MAINTAINER antoniorossi <antoniorossi@outlook.com>

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data

COPY magento-1.5.1.0-2015-02-12-06-33-41.tgz /
RUN tar xvzf magento-1.5.1.0-2015-02-12-06-33-41.tgz
RUN rm -rf /var/www/magento
RUN mv magento /var/www
RUN rm magento-1.5.1.0-2015-02-12-06-33-41.tgz
RUN chown -R $APACHE_RUN_USER:$APACHE_RUN_GROUP /var/www/magento

VOLUME ["/var/www/magento"]
VOLUME ["/var/www/magento/media"]
