FROM debian:latest


MAINTAINER liangjia (liangjia1989@hotmail.com)

RUN	apt-get update \
	&& apt-get install -y cmake \
    && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && ldconfig
