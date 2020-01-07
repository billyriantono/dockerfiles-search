FROM linuxconfig/lamp
MAINTAINER Lubos Rendek <web@linuxconfig.org>

# Install prerequisites 
RUN apt-get install -y wget

# Download and unzip Drupal
RUN wget -qO /tmp/drupal.tar.gz http://ftp.drupal.org/files/projects/drupal-7.37.tar.gz
RUN rm -fr /var/www/html
RUN gunzip -c /tmp/drupal.tar.gz | tar x -C /tmp/
RUN rm /tmp/drupal.tar.gz
RUN mv /tmp/drupal-* /var/www/html

# Create database
RUN service mysql start; mysqladmin -uadmin -ppass create drupal

# Apache configuration
ADD 000-default.conf /etc/apache2/sites-available/
RUN a2enmod rewrite


# Update file and directory ownership
RUN chown -R www-data.www-data /var/www/html

# Allow ports
EXPOSE 80

CMD ["supervisord"]