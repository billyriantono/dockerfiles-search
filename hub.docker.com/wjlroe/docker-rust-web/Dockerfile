FROM wjlroe/docker-ubuntu-rust:latest
MAINTAINER William Roe "git@wjlr.org.uk"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
	apt-get install \
	build-essential \
	uuid-dev \
	libssl-dev \
	-qqy \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV LAST_RUST_IMAGE_UPDATE=2018-07-22

RUN rustc --version
