#Dockerfile for apache2
FROM alpine:latest
MAINTAINER Mikolaj Kaja <kontakt AT mikolajkaja DOT pl>

#Install apache2 and create directory for apache
RUN apk --update add apache2 php5-apache2 &&\
	mkdir -p /run/apache2

#Open 80 port
EXPOSE 80

#To run apache2 in foreground execute:
CMD ["/usr/sbin/httpd","-D", "FOREGROUND"]
