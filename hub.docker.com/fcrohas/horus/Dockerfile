FROM ubuntu:xenial

MAINTAINER Fabrice Crohas <fcrohas@gmail.com>

RUN apt-get update
RUN apt-get dist-upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install python-software-properties
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install software-properties-common

RUN add-apt-repository ppa:bqlabs/horus-dev && apt-get update

RUN apt-get -y install horus 

VOLUME /root/.horus

CMD ["horus"]
