FROM ubuntu:14.04
MAINTAINER Ping Dong (ping.dong@live.com)

LABEL version="1.0"
LABEL last-modified="03/09/2015 12:00PM"

# UPDATE
RUN apt-get -y update
RUN apt-get -y dist-upgrade

# SETUP APACHE
RUN apt-get -y install apache2 

ENV APACHE_RUN_USER www-data 
ENV APACHE_RUN_GROUP www-data 
ENV APACHE_LOG_DIR /var/log/apache2 
ENV APACHE_PID_FILE /var/run/apache2.pid 
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# FIREWALL
EXPOSE 80

# START
ENTRYPOINT ["/usr/sbin/apache2"] 
CMD ["-D", "FOREGROUND"]  