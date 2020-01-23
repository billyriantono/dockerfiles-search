FROM ubuntu:16.04

ARG MAKEFLAGS=-j8

RUN apt-get update && apt-get install -y \
  autoconf \
  automake \
  build-essential \
  curl \
  git \
  default-jdk \
  default-jre \
  libtool \
  libpcre3-dev \
  libssl-dev \
  make \
  nginx \
  zip \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt-get install -y nodejs \
	&& rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/grpc/grpc-web /github/grpc-web \
	&& cd /github/grpc-web \
	&& ./scripts/init_submodules.sh \
	&& cd /github/grpc-web/third_party/grpc \
	&& make && make install \
	&& cd /github/grpc-web/third_party/grpc/third_party/protobuf \
	&& make install \
	&& cd /github/grpc-web \
	&& make install-plugin \
	&& rm -rf /github
