FROM linuxconfig/lamp
MAINTAINER Lubos Rendek <web@linuxconfig.org>

# Install prerequisites 
RUN apt-get update
RUN apt-get install -y wget

# Insert a repository to get the latest ownCloud version
RUN wget -q http://download.opensuse.org/repositories/isv:ownCloud:community/Debian_8.0/Release.key
RUN apt-key add - < Release.key
RUN echo 'deb http://download.opensuse.org/repositories/isv:/ownCloud:/community/Debian_8.0/ /' >> /etc/apt/sources.list.d/owncloud.list
RUN apt-get update

# Install owncloud
RUN apt-get install -y ownCloud

# Create a database
RUN service mysql start; mysqladmin -uadmin -ppass create owncloud

# Configure Apache
RUN a2dissite 000-default
RUN sed -i '0,/owncloud/s///' /etc/apache2/conf-available/owncloud.conf

# Allow ports
EXPOSE 80

CMD ["supervisord"]
