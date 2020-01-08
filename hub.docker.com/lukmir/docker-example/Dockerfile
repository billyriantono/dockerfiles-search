FROM ubuntu:16.04
MAINTAINER lukmir
RUN apt-get update 
RUN apt-get install -y apache2 
RUN apt-get clean
ENV APACHE_LOG_DIR /var/log/apache2
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
