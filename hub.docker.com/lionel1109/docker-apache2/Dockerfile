# Base image is Ubuntu
FROM ubuntu:16.04

# Author: 
MAINTAINER H. Meftah <dockerlite@gmail.com>

# Install apache2 package
RUN apt-get update && \
apt-get install -y apache2 && \
apt-get clean
Expose 80
# Set the log directory PATH
ENV APACHE_LOG_DIR /var/log/apache2

# Launch apache2 server in the foreground
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

