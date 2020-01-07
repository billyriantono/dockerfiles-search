# DOCKER-VERSION 1.10.3
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/ubuntu-sshd

FROM ubuntu:14.04
MAINTAINER Yong Zhang<zhangyong.net@qq.com>

RUN apt-get update
RUN apt-get install -y openjdk-7-jdk
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:rootroot' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22 
CMD ["/usr/sbin/sshd", "-D"]
