FROM debian:jessie
MAINTAINER ripisu2003@gmail.com
RUN apt-get update && \
    apt-get -y install apache2 php5 php5-mysql php5-gd libapache2-mod-php5 

ENTRYPOINT [ "/usr/sbin/apachectl", "-D", "FOREGROUND" ]


