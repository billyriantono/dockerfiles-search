FROM ubuntu:18.04

MAINTAINER fujiwaraizuho

RUN echo "Make Vreath Directory..." && \
	mkdir /home/vreath

WORKDIR /home/vreath

RUN echo "Ubuntu package update & upgrade..." && \
	apt-get update && \
	apt-get upgrade -y

RUN echo "Install utilities..." && \
	apt-get install -y --no-install-recommends \
  	dconf-tools \
  	apt-transport-https software-properties-common ppa-purge apt-utils \
  	ca-certificates git curl wget \
  	tar zip unzip zlib1g-dev bzip2 libbz2-dev \
  	openssl libssl-dev \
  	zsh vim screen tree htop \
  	net-tools lynx iftop traceroute \
  	build-essential python

RUN echo "Install nodebrew..." && \
	curl -L git.io/nodebrew | perl - setup

ENV PATH /root/.nodebrew/current/bin:$PATH

ENV NODE_VERSION v11.13.0

RUN echo "Install Node v11.13.0+..." && \
	nodebrew install ${NODE_VERSION} && \
	nodebrew use ${NODE_VERSION}

RUN echo "Check Node & NPM version..." && \
	node -v && \
	npm -v

RUN echo "Install yarn v1.17.3+..." && \
	npm install -g yarn

RUN echo "Check yarn version..." && \
	yarn -v

ENV RUST_VERSION stable

RUN echo "Install cargo rustup rustc..." && \
	curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain ${RUST_VERSION}

ENV PATH /root/.cargo/bin:$PATH

RUN echo "Check cargo & rustup & rustc..." && \
	cargo -V && \
	rustup -V && \
	rustc -V

RUN echo "Change the version of rustc into nightly..." && \
	rustup default nightly

RUN echo "Clone vreath-cli..." && \
	git clone https://github.com/Vreath-core/vreath-cli.git

WORKDIR vreath-cli

RUN echo "Build vreath-cli..." && \
	yarn build && \
	yarn link