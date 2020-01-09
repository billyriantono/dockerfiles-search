FROM ubuntu:trusty
MAINTAINER stefanzweig

RUN echo "deb http://opensource.nchc.org.tw/ubuntu/ trusty main multiverse restricted universe" > /etc/apt/sources.list
RUN echo "deb http://opensource.nchc.org.tw/ubuntu/ trusty-backports main multiverse restricted universe" >> /etc/apt/sources.list
RUN echo "deb http://opensource.nchc.org.tw/ubuntu/ trusty-proposed main multiverse restricted universe" >> /etc/apt/sources.list
RUN echo "deb http://opensource.nchc.org.tw/ubuntu/ trusty-security main multiverse restricted universe" >>/etc/apt/sources.list
RUN echo "deb http://opensource.nchc.org.tw/ubuntu/ trusty-updates main multiverse restricted universe" >> /etc/apt/sources.list

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y tar
RUN apt-get install -y git
RUN apt-get install -y curl
RUN apt-get install -y nano
RUN apt-get install -y wget
RUN apt-get install -y dialog
RUN apt-get install -y net-tools
RUN apt-get install -y build-essential
RUN apt-get install -y nginx  sed supervisor
RUN apt-get install -y python2.7 \
    python2.7-dev \
    python-distribute \
    python-pip \
    uwsgi-plugin-python

RUN pip install -U pip

RUN pip install -U Flask
RUN pip install -U robotframework

RUN env --unset=DEBIAN_FRONTEND

EXPOSE 5000 22
