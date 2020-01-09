FROM ubuntu:18.04
MAINTAINER Shildra<shildra>

# Avoiding user interaction with tzdata
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y apache2 # Install Apache webserver (Only 'yes')
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y php5.6

# connect PHP & MySQL
RUN apt-get install -y php5.6-mysql

EXPOSE 80
CMD ["apachectl", "-D", "FOREGROUND"]

