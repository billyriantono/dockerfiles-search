FROM ubuntu:14.04

ARG MESOS_VERSION=1.2.0
ENV DISTRO=ubuntu
ENV CODENAME=trusty

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF
RUN echo "deb http://repos.mesosphere.com/${DISTRO} ${CODENAME} main" | \
    tee /etc/apt/sources.list.d/mesosphere.list && \
    apt-get -y update
RUN apt-get -y install mesos
RUN mkdir /opt/mesos

WORKDIR /opt/mesos