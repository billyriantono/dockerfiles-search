# Devcarpet docker file
FROM ubuntu:16.04
MAINTAINER Rafał bluszcz Zawadzki <bluszcz@decarpet.net>
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install python3-dev wget -y
RUN cat /etc/hosts
RUN apt-get install slapd -y                                                     
