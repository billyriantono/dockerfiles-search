FROM ubuntu:latest
MAINTAINER Vali Malinoiu <0x4139@gmail.com>

#install java 8
RUN mkdir -p /opt/jre
COPY jre-8u45-linux-x64.tar.gz /tmp/
RUN tar -zxf /tmp/jre-8u45-linux-x64.tar.gz -C /opt/jre
RUN update-alternatives --install /usr/bin/java java /opt/jre/jre1.8.0_45/bin/java 100

#cleanup
RUN rm -rf /tmp/*
