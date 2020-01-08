FROM ubuntu
MAINTAINER kvgarnet for Docker
RUN apt-get update
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo "root:123456" | chpasswd
EXPOSE 22


