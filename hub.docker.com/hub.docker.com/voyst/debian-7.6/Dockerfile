FROM debian:7.6
RUN apt-get update
RUN apt-get upgrade
RUN apt-get -y install vim
RUN apt-get -y install curl
RUN apt-get -y install git-core
RUN apt-get -y install openssh-server
RUN apt-get -y install ssh
RUN apt-get -y install sudo
RUN apt-get -y install ntp
run apt-get -y install socat
RUN /etc/init.d/ntp start
