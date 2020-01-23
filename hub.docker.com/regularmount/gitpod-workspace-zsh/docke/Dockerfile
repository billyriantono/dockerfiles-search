FROM ubuntu



MAINTAINER Ryan Coughlan <rcoughlan90@gmail.com>

RUN apt-get update && apt-get install -y openssh-server

RUN mkdir -p /var/run/sshd
ADD sshd_config /etc/ssh/sshd_config
cmd /usr/sbin/sshd -D
