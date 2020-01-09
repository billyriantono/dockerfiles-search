FROM ubuntu:14.04
MAINTAINER Sean Liu <liouys@gmail.com>

ENV DEBIAN_FRONTEND noninteractive 
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN apt-get -y update
RUN apt-get -q -y install git-core python python-pip vim curl sudo
RUN apt-get -y install openssh-server
RUN mkdir -p /var/run/sshd
RUN useradd -d /home/admin -m -s /bin/bash admin
RUN echo 'admin:docker' | chpasswd
RUN echo 'root:docker' | chpasswd
RUN echo 'admin ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/admin
RUN chmod 0440 /etc/sudoers.d/admin

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

