FROM ubuntu:16.04
MAINTAINER Vitor Hugo <info@deployer.pt>

# install Apache
RUN apt-get update && \
    apt-get install -y apache2 && \
    rm -rf /var/lib/apt/lists/*

# start Apache
RUN service apache2 start

# set up Apache environment variables
ENV APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_LOCK_DIR=/var/lock/apache2 \
    APACHE_PID_FILE=/var/run/apache2.pid

EXPOSE 80
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]