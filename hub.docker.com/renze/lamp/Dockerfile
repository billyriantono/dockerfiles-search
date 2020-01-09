# Ubuntu 14.04 LAMP
#
# Create an ubuntu LAMP stack and configure MySQL with persistent data storage
#
# Forked from tutum-docker-lamp by Fernando Mayo <fernando@tutum.co>

# use newest LTS as base
FROM ubuntu:14.04
MAINTAINER Renze van der Kamp <git@renzevanderkamp.nl>

# Set UTF-8 locale
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# Package installation
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
	DEBIAN_FRONTEND=noninteractive apt-get -y install \
		supervisor \
		apache2 \
		libapache2-mod-php5 \
		mysql-server \
		php5-mysql \
		php5-mcrypt \
		pwgen 
		
# Supervisor
# Add to supervisor
ADD supervisord-apache2.conf /etc/supervisor/conf.d/supervisord-apache2.conf
ADD supervisord-mysqld.conf /etc/supervisor/conf.d/supervisord-mysqld.conf

# MySQL
# Configure MySQL to listen to all and to use datadir /data
ADD my.cnf /etc/mysql/conf.d/my.cnf

# Decouple our data from our container.
VOLUME ["/data"]

# add scripts
ADD scripts /scripts
RUN chmod -R 755 /scripts

# phpmyadmin
RUN /scripts/phpmyadmin/install.sh

EXPOSE 80 3306

CMD ["/scripts/run.sh"]
