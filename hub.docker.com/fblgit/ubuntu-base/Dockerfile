#name of container: ubuntu-base
#version of container 0.1
FROM ubuntu:14.04.3
MAINTAINER FBLGIT
VOLUME /data
COPY files/ubuntu-apt.sh /data/ubuntu-apt.sh
COPY files/ubuntu-apt.list /data/ubuntu-apt.list
RUN chmod +x /data/ubuntu-apt.sh && /data/ubuntu-apt.sh
RUN apt-get install -qy wget dstat
