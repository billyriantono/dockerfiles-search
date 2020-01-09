FROM debian:9-slim

LABEL maintainer="serpi90@gmail.com"

RUN apt-get update \
	&& apt-get --assume-yes --no-install-recommends install pandoc \
	&& apt-get clean \
	&& rm --recursive --force /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data
VOLUME ["/data"]

