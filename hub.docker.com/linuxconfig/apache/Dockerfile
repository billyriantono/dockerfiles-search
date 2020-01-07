FROM debian:9
MAINTAINER Lubos Rendek <web@linuxconfig.org>

# Update package Repository
RUN apt-get update

# Apache web server installation
RUN apt-get -y install apache2

EXPOSE 80

CMD echo "ServerName `hostname`" >> /etc/apache2/apache2.conf; /usr/sbin/apache2ctl -DFOREGROUND
