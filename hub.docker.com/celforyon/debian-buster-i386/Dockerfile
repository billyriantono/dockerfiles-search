FROM debian:buster

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="toolchain for Debian buster i386"

RUN  dpkg --add-architecture i386 \
	&& apt update \
	&& apt install -y --no-install-recommends --no-install-suggests \
		make cmake git catch gcc:i386 g++:i386 \
	&& rm -rf /var/lib/apt/lists/*
