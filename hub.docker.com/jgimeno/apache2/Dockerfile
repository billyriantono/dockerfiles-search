FROM ubuntu:14.04

MAINTAINER Jonathan Gimeno <jgimeno@gmail.com>

# Install apache2 package
RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean

# Set the log directory PATH
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80

# Launch apache2 server in the foreground
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]