FROM debian:jessie
MAINTAINER Guillaume Lhermenier <guillaume.lhermenier@gmail.com>

RUN apt-get update \
	&& apt-get install -y texlive-full \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir /var/inputs

WORKDIR /var/inputs

CMD xelatex
