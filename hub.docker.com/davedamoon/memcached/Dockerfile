FROM        ubuntu:14.04
MAINTAINER  David Sauer davedamoon@gmail.com

ENV MEM 64
EXPOSE 11211

RUN apt-get update;
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y;
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget curl memcached

USER daemon
CMD memcached -m $MEM
