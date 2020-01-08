FROM ubuntu:16.04

MAINTAINER Maurice de Vries <>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install mosquitto mosquitto-clients -y

EXPOSE 1883
CMD ["/usr/sbin/mosquitto"]