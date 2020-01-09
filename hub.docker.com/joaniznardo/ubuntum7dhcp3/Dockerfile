#FROM ubuntu:14.04

FROM joaniznardo/ubuntum7base

MAINTAINER joaniznardo (github)

ENV DEBIAN_FRONTEND=noninteractive
#RUN apt-get update && apt-get install -y openssh-server sudo supervisor
#RUN useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo
RUN apt-get install -q -y -o "DPkg::Options::=--force-confold" -o "DPkg::Options::=--force-confdef" isc-dhcp-relay 

CMD /etc/init.d/ssh restart && supervisord -n
