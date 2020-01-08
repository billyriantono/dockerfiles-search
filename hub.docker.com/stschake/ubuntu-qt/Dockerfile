FROM ubuntu:trusty
MAINTAINER Stefan Schake <stschake@gmail.com>

RUN apt-get update -qq
RUN apt-get -y install build-essential software-properties-common
RUN apt-get -y install fuse wget zlib1g-dev libgl1-mesa-dev git
RUN add-apt-repository ppa:beineri/opt-qt591-trusty -y
RUN apt-get update -qq
RUN apt-get -y install qt59base qt59multimedia qt59tools qt59imageformats qt59script qt59graphicaleffects qt59quickcontrols qt59quickcontrols2

