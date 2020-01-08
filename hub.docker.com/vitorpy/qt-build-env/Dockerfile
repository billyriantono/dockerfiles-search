FROM ubuntu:xenial
MAINTAINER Vitor Py

RUN apt-get update -y
RUN apt-get install software-properties-common python-software-properties -y; true
RUN apt-get install apt -y
RUN add-apt-repository ppa:beineri/opt-qt-5.10.0-xenial
RUN apt-get update -y
RUN apt-get install qt510-meta-full -y
RUN apt-get install -y build-essential
RUN /opt/qt510/bin/qt510-env.sh 
