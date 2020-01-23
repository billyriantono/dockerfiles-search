FROM ubuntu:14.04
MAINTAINER Tanya Gray (t.gray@auckland.ac.nz)

RUN apt-get update 

ENV DEBIAN_FRONTEND noninteractive

# install common tools to allow add-apt-repository
RUN apt-get install -y software-properties-common

# install desktop environment
RUN apt-get install -y xfce4 --no-install-recommends xfce4-goodies

# install openssh for remote access
RUN apt-get install -y openssh-server

# install x2go for desktop access via x2goClient app
RUN add-apt-repository ppa:x2go/stable
RUN apt-get update
RUN apt-get install x2goserver x2goserver-xsession pwgen -y


# allow shell access
EXPOSE 22