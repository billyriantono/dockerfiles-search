FROM golang:latest

LABEL maintainer="Stephen Hohls & Truevolve Technologies"
LABEL version="REPLACE_WITH_BITBUCKET_VERSION"
LABEL description="Golang image with Python3 included"

RUN apt update
RUN apt install -y \
	bash \
	curl \
	git \
	nano \
	python3 \
	tar \
	unzip \
	vim \
	wget

CMD /bin/bash
