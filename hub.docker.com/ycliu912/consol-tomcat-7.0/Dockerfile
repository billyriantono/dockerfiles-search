FROM tomcat:7-jre7
MAINTAINER "ycliu <ycliu1283@gmail.com>"
RUN echo "root:root" | chpasswd
RUN apt-get update &&  apt-get install -y openssh-server vim  && mkdir /var/run/sshd && /usr/sbin/sshd
EXPOSE 22
