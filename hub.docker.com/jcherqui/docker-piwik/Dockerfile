FROM debian:jessie

ENV PIWIK_VERSION 3.0.4

# Variables d'environnement
ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No

# Dependencies
RUN apt-get update --fix-missing
RUN apt-get install -y apt-utils debconf-utils dialog locales
RUN apt-get update
RUN apt-get install -y apache2 php5 php5-gd php5-mysql wget unzip

# Piwik
RUN rm -R /var/www/html
RUN cd /var/ && wget http://builds.piwik.org/piwik.zip
RUN cd /var/ && wget https://builds.piwik.org/piwik-${PIWIK_VERSION}.zip
RUN cd /var/ && unzip piwik.zip && rm piwik.zip
RUN mv /var/piwik /var/www/html
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 0755 /var/www/html/tmp

# PHP
RUN sed -i -e "s/;always_populate_raw_post_data/always_populate_raw_post_data/g" /etc/php5/apache2/php.ini

# Apache2
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2

EXPOSE 80
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
