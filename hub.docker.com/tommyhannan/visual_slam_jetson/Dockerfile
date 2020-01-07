FROM tommyhannan/ubuntu_slam

MAINTAINER Tommy Hannan <tommy@rollomotion.com>

WORKDIR /opt

RUN cd /opt \
&& git clone https://github.com/rollo/rollo_slam \
&& cd rollo_slam && chmod +x build-docker.sh && sh build-docker.sh
