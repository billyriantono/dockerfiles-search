# This is a custom ubuntu image with SSH installed
#

FROM ubuntu:trusty
MAINTAINER byunique <me@brandonyu.com>

RUN apt-get update -y
RUN apt-get install apache2 -y
RUN apt-get install curl -y
RUN apt-get install telnet -y
RUN echo "/usr/sbin/service apache2 start" >> /root/.bashrc

EXPOSE 80:8000
