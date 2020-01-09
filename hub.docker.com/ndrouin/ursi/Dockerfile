FROM centos:latest 
MAINTAINER Nico

WORKDIR /root

#change sh to bash
RUN yum update -y
RUN yum install java-1.8.0-openjdk -y
RUN yum install bash -y

#add files
ADD epita.jar /root
ADD nohup.out /root
ADD readme.txt /root
ADD start.sh /root
ADD logs.txt /root

#set permissions
RUN chmod +x start.sh

#firewall
EXPOSE 8080
