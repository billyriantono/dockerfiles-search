FROM ubuntu:16.04
MAINTAINER Gines Espada <gines.espada@gmail.com>

# Install dependencies, needed packages, and gcc required toolchains
RUN DEBIAN_FRONTEND=noninteractive \
	apt-get update && apt-get install -yq curl git file apt-utils build-essential \
	gcc-arm-linux-gnueabi \
	gcc-arm-linux-gnueabihf \
	gcc-aarch64-linux-gnu
RUN apt-get clean

# Install Multirust
RUN git clone --recursive https://github.com/brson/multirust \
	&& cd multirust && git submodule update --init \
	&& ./build.sh && ./install.sh \
	&& multirust default stable \
	&& multirust update stable

# Install targets
RUN multirust add-target stable arm-unknown-linux-gnueabi \
	&& multirust add-target stable arm-unknown-linux-gnueabihf \
	&& multirust add-target stable armv7-unknown-linux-gnueabihf \
	&& multirust add-target stable aarch64-unknown-linux-gnu

# Working directory for the rust projects
RUN mkdir /workspace
VOLUME ["/workspace"]
WORKDIR /workspace

# Default command gets into the shell
CMD ["/bin/bash"]