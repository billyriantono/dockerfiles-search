FROM krmit/ssh 
MAINTAINER Magnus Kronnäs 

################################################################
#       Apace server                                           #
################################################################
# Inspired by https://registry.hub.docker.com/u/eboraas/apache

# Install Apache-server
RUN apt-get install -y apache2

# Config envoriment variables for  
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

# Create a mount point for all webpage
VOLUME ["/root/"]

# Remove html directory so it could be replace with a symlink. 
RUN rm -r /var/www/html

################################################################
#        PHP lang                                              #
################################################################

RUN apt-get install -y \
       php5 \
       libapache2-mod-php5 \ 
       php5-mcrypt \
       php5-mysql

################################################################
#       Initiate                                               #
################################################################

# Open up ssh port.
EXPOSE 80

# Start the ssh  && /usr/sbin/mysqld
# The root mount point must contain a subfolder "www" for webcontent.
# sshd and only it, since it is the last command, must be in the foreground. 
CMD ln -s /root/www /var/www/html; /usr/sbin/apache2ctl start && /usr/sbin/sshd -D
