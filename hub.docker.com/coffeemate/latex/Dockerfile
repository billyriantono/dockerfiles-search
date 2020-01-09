FROM ubuntu:16.04

MAINTAINER himuhasib@gmail.com

RUN apt-get update && apt-get install -y \
		build-essential \
		libfontconfig1 \
		python2.7 \
		tzdata \
		wget

COPY install.sh install.sh
RUN chmod u+x install.sh && ./install.sh
RUN rm install.sh

ENV PATH="/usr/local/texlive/2018/bin/x86_64-linux:$PATH"

RUN rm -rf /var/lib/apt/lists/*
