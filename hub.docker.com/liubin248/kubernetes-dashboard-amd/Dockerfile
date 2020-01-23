FROM ubuntu:latest

COPY smb.conf /etc/samba/smb.conf

#
# proxy
#

#ENV http_proxy  "http://web-proxy.sgp.hpecorp.net:8080"
#ENV https_proxy "http://web-proxy.sgp.hpecorp.net:8080"

#
# apt
#

RUN apt-get update
#RUN apt-get upgrade
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install -y android-sdk
RUN apt-get install -y apt-utils
RUN apt-get install -y build-essential
RUN apt-get install -y curl
RUN apt-get install -y dnsutils
RUN apt-get install -y git
RUN apt-get install -y htpdate
RUN apt-get install -y iputils-ping
RUN apt-get install -y joe
RUN apt-get install -y lftp
RUN apt-get install -y mongodb
RUN apt-get install -y nano
RUN apt-get install -y net-tools
RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN apt-get install -y openssh-client
RUN apt-get install -y openssh-server
RUN apt-get install -y postgis postgresql
RUN apt-get install -y pdsh
RUN apt-get install -y python
RUN apt-get install -y python-pip
RUN apt-get install -y samba
RUN apt-get install -y ssh
RUN apt-get install -y telnet
RUN apt-get install -y unrar
RUN apt-get install -y unzip
RUN apt-get install -y vim
RUN apt-get install -y wget
RUN ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

#
# git
#

RUN git config --global user.name "limulidae"
RUN git config --global user.email "limulidae@gmail.com"

#
# npm
#

RUN npm config set depth=0
RUN npm -g install mocha

#
# Samba
#
# gpedit.msc
# Computer Configuration>Administrative Templates > Network > Lanman Workstation
# open "Enable insecure guest logons" and choose Enabled. 

EXPOSE 139
EXPOSE 445

#
# SQL
#

EXPOSE 5432

RUN echo listen_addresses = \'*\' >> /etc/postgresql/10/main/postgresql.conf

#
# SSH
#

EXPOSE 22

#
# users
#

RUN useradd -m -s /bin/bash limulidae

#
# development
#

#
# start up
#

ENTRYPOINT /etc/init.d/nmbd restart && \
#           /etc/init.d/postgresql restart && \
           /etc/init.d/smbd restart && \
           /etc/init.d/ssh restart && \
           /bin/bash
