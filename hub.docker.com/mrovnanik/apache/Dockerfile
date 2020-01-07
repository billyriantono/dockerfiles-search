FROM httpd:2.4
MAINTAINER Michal Rovnanik <michal@rovnanik.sk>

# upload new config
COPY ./config/vi-srv-httpd.conf /usr/local/apache2/conf/httpd.conf

#install vim
RUN apt-get update
RUN apt-get install vim -y
RUN apt-get clean