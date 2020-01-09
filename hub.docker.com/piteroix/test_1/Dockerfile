FROM ubuntu
LABEL maintainer="pawlakPiotr@gm.com"
RUN  apt-get update
RUN apt-get -y install apache2
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf
RUN service apache2 start
