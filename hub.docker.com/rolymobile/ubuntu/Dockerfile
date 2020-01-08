FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN \
	apt-get update -qqy && \
	apt-get -qqy upgrade && \
	apt-get install -qqy wget vim && \
	rm -rf /var/lib/apt/lists/*
CMD bash
