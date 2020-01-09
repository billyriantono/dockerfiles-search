FROM ubuntu:trusty
MAINTAINER Mhd Sami Almouhtaseb <mssatnami@gmail.com>

RUN apt-get update 
RUN apt-get dist-upgrade -y
RUN apt-get install -y net-tools vim nano vpnc ssh

ADD default.conf /etc/vpnc/default.conf