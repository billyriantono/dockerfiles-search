FROM php:7.0-apache
# Make Apache run on port 8080 and as user www-data
RUN sed -i -e 's/80/8080/' /etc/apache2/ports.conf /etc/apache2/sites-available/000-default.conf
# Change PID location to a writeable location.
RUN sed -i -e 's+: ${APACHE_PID_FILE:=/var/run/apache2/apache2$SUFFIX.pid}+: ${APACHE_PID_FILE:=/tmp/apache2$SUFFIX.pid}+' /etc/apache2/envvars
# Make /var/lock/apache2 writeable by www-data
RUN chown www-data:www-data -R /var/lock/apache2
# For testing. No idea if it helps.
RUN chmod 777 -R /var/lock/apache2
USER www-data
EXPOSE 8080
COPY src/ /var/www/html/
