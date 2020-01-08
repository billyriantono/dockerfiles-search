# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER trukhinyuri <yuri@trukhin.com>
ENV REFRESHED_AT 2014–11–03
RUN apt-key update
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install apache2
RUN apt-get clean
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
EXPOSE 80
EXPOSE 443
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]