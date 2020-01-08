#################################################
# Debian with added nagios3 Server.
# Basic Nagios3 without plugins.
#################################################

# Using latest debian image as base
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

ENV DEBIAN_FRONTEND noninteractive

# install dependancies
RUN apt-get update && apt-get install -y nagios3

#configure nagios3.conf
COPY nagios3.conf /etc/apache2/conf.d/

#configure nagios.cfg
COPY nagios.cfg /etc/nagios3/

#configure nagios password default
# htpasswd -c -b  /etc/nagios/htpasswd.users nagiosadmin admin
COPY htpasswd.users /etc/nagios3/

#configure ports.conf
COPY ports.conf /etc/apache2/


# startup
ADD start.sh /start.sh
RUN chmod 0755 /start.sh
CMD ["bash", "start.sh"]

EXPOSE 8080/tcp
