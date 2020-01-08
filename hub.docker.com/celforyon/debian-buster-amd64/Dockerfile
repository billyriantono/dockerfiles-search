FROM debian:buster

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="toolchain for Debian buster amd64"

RUN  apt update \
	&& apt install -y --no-install-recommends --no-install-suggests \
		make cmake git catch gcc g++ \
	&& rm -rf /var/lib/apt/lists/*
