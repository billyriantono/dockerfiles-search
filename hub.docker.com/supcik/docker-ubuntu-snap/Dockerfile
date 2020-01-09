FROM ubuntu
MAINTAINER Jacques Supcik <jacques@supcik.net>

RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
		patch \
		scons \
		pkg-config \
		ca-certificates \
		curl \
		python \
		git \
		gcc-arm-linux-gnueabihf \
		binutils-arm-linux-gnueabihf \
		snapcraft \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /
