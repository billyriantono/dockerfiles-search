#
# Dockerfile for creating a docker image that runs Visualink Pastec. An image
# search index.
#
# You can map the data volume to a local share. Be sure to put the
# visualWordsORB.dat file in that folder before loading the docker image.
#
# A C# implementation for accessing the API is available at:
#    https://github.com/CasperCDR/CsPastecLib
#
# Date: 25 Nov 2019
#
FROM ubuntu:18.04

ENV TZ=Europe/Amsterdam
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
  && echo $TZ > /etc/timezone \
  && apt update \
  && apt upgrade -y --force-yes \
  && apt install -y wget curl build-essential g++ libcurl4-openssl-dev libopencv-dev libmicrohttpd-dev libjsoncpp-dev cmake git \
  && git clone https://github.com/Visu4link/pastec.git \
  && mkdir -p /pastec/build \
  && mkdir /pastec/data \
  && cd /pastec/data \
  && wget http://pastec.io/files/visualWordsORB.tar.gz \
  && tar zxf visualWordsORB.tar.gz \
  && cd /pastec/build \
  && cmake ../ && make

WORKDIR /pastec/build

EXPOSE 4212
VOLUME /pastec/data

CMD ./pastec -p 4212 /pastec/data/visualWordsORB.dat
