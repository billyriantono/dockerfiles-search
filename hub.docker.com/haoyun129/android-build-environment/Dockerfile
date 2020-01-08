FROM ubuntu:16.04
MAINTAINER Hao-Yun Yin "haoyun.tw@gmail.com"

#ENV LANG en_US.UTF-8
#RUN locale-gen $LANG
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install --assume-yes apt-utils

RUN apt-get -y install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip

RUN apt-get -y install software-properties-common
RUN apt-add-repository ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get -y install openjdk-8-jdk

RUN apt-get -y install mkisofs git python bc libssl-dev repo
RUN apt-get -y install vim bsdmainutils

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
ENV USER root

