FROM clouder/clouder-base
MAINTAINER Yannick Buron yburon@goclouder.net

RUN usermod -u 1000 www-data

# Create saved folders
RUN mkdir -p /opt/magento/exec/var/log
RUN mkdir -p /opt/magento/exec/app/etc
RUN mkdir -p /opt/magento/exec/app/code/local
RUN mkdir -p /etc/apache2/sites-enabled

# Adding configuration files
RUN mkdir -p /opt/magento/config
ADD sources/config.xml /opt/magento/config/config.xml
ADD sources/magento.conf /etc/apache2/sites-enabled/magento.conf

# Switching rights
RUN chown -R www-data:www-data /opt/magento
