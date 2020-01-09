FROM ubuntu:latest

MAINTAINER Johann Förster <johann.foerster@qualityminds.de>

RUN export DEBIAN_FRONTEND=noninteractive && \
	apt-get update && \ 
	apt-get install -y  \
	git sudo tzdata wget && \
	rm -rf /var/lib/apt/lists/* 

RUN useradd -m --shell /bin/bash compiler && \
    echo "compiler ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/compiler && \
    chmod 0440 /etc/sudoers.d/compiler

USER compiler

RUN whoami