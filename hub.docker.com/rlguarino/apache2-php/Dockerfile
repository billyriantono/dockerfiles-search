#
# Dockerfile - Apache-PHP
#
# A simple php + apache container.

FROM ubuntu:quantal
MAINTAINER Ross Guarino <rssguar@gmail.com>

# Install packages.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install supervisor apache2 libapache2-mod-php5

# Add configuration scripts.
ADD supervisord-apache2.conf /etc/supervisor/conf.d/supervisor-apache2.conf
ADD start-apache2.sh /start-apache2.sh
RUN chmod 755 /*.sh
RUN ln -s /var/www/ /app

EXPOSE 80