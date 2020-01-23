FROM ubuntu:12.04
MAINTAINER Erik van Roode <erikvroode@gmail.com>

# Install packages
RUN apt-get update
RUN apt-get install -y apache2

# Add image configuration
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]

