FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y vim git nodejs npm

RUN npm install libp2p libp2p-tcp peer-info async @nodeutils/defaults-deep pull-stream \
  libp2p-websockets

# work dir
RUN mkdir /root/work
ADD *.js /root/work/

WORKDIR /root/work

