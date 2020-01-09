FROM ubuntu:latest
MAINTAINER Scott Pepper <scott-docker@pep.id.au>
# Create a debug container for a cosmos-aware environment
RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apache2 php php-mysql libapache2-mod-php curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/ && \
    a2enmod rewrite && \
    sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php/7.2/apache2/php.ini
# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
COPY apache2.conf /etc/apache2/apache2.conf
# Expose apache.
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND > /dev/stdout
