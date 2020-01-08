FROM ubuntu:12.04
MAINTAINER Mats Norén, mats.noren@gmail.com

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y build-essential git cmake pkg-config libprotoc-dev libprotobuf7
RUN apt-get install -y protobuf-compiler libprotobuf-dev libosmpbf-dev libpng12-dev
RUN apt-get install -y libbz2-dev libstxxl-dev libstxxl-doc libstxxl1 libxml2-dev
RUN apt-get install -y libzip-dev libboost-all-dev lua5.1 liblua5.1-0-dev libluabind-dev libluajit-5.1-dev

RUN git clone https://github.com/DennisOSRM/Project-OSRM.git

RUN mkdir -p Project-OSRM/build;cd Project-OSRM/build; cmake ..; make