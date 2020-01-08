# Simple HTTP only WebDAV / Apache2
# ----------------------------------
# Version:	0.1
# AUTHER:	Jaspalsinh Chauhan
# EMAIL:	jachauhan@gmail.com
# ----------------------------------

FROM ubuntu:14.04
MAINTAINER Jaspalsinh Chauhan <jachauhan@gmail.com>

# Set build / run mode as non-interactive
ENV DEBIAN_FRONTEND noninteractive

# Update package manager
RUN apt-get update
# Install Apache2 web server (non-interactive)
RUN apt-get -y install apache2

# Enable WebDAV apache modules
RUN a2enmod dav
RUN a2enmod dav_fs

# Remove default 000-default.conf file added by Apache2 on install
RUN rm /etc/apache2/sites-enabled/000-default.conf
# Add this container's 000-default.conf
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

# Create webdav root folder
RUN mkdir /var/www/webdav
# Set permission for apache2 web server to webdav root folder
RUN chown -R www-data:www-data /var/www/

# You know right?
EXPOSE 80

# Restart apache webserver
RUN service apache2 stop
RUN service apache2 start
