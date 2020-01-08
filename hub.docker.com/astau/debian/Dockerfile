# Debian base image - 8.6 
FROM debian:8.6

MAINTAINER Srikanth <srikanth@astau.com>

RUN apt-get update && apt-get -y install \
	ca-certificates \
	curl \
	tar \
	bzip2 \
	xz-utils \
	libglib2.0-0 \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*