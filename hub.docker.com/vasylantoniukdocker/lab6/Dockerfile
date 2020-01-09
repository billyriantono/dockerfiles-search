FROM ubuntu
MAINTAINER Vasyl Antoniuk
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y apache2
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
