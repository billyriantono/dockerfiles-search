FROM ubuntu:14.04
MAINTAINER Vincent Rijlaarsdam "rijlvl1@student.op.ac.nz"

# Update and upgrade
RUN apt-get -yqq update
RUN apt-get -yqq upgrade

# Install apache2
RUN apt-get -yqq install apache2

# Install supervisor
RUN apt-get -yqq install supervisor

# Add supervisor file
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Set working directory
WORKDIR /var/www/html

# Apache specific commands
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

# Apache specific directories
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

# Expose port 80
EXPOSE 80

# Supervisor for apache
CMD ["/usr/bin/supervisord"]