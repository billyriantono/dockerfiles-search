FROM phusion/baseimage:0.9.22
MAINTAINER Wira Rohandi <wira@rohandi.com>

RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y -q unzip openjdk-8-jdk git mercurial subversion maven wget nano

# Enable SSH
RUN rm -f /etc/service/sshd/down

# Possibility to add a public key
# ADD ssh_key.pub /tmp/ssh_key.pub
# RUN cat /tmp/ssh_key.pub >> /root/.ssh/authorized_keys && rm -f /tmp/ssh_key.pub

# Clean up
WORKDIR /tmp
RUN apt-get clean

EXPOSE 22

CMD ["/sbin/my_init"]