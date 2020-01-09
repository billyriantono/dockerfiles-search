FROM ubuntu:14.04
ENV DEBIAN_FRONTEND noninteractive
ENV NAGIOS_SERVER 127.0.0.1
RUN apt-get update && apt-get -y install vim git nagios-nrpe-server
ADD nrpe.cfg /etc/nagios/nrpe.cfg
EXPOSE 5666
