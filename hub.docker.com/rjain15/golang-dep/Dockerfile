FROM golang:alpine AS builder
MAINTAINER Rajesh Jain <rjain15@gmail.com>
RUN apk update
RUN apk upgrade

RUN apk add --no-cache curl openssl
RUN apk add --no-cache wget
RUN apk add --update --no-cache bash
RUN apk add --update --no-cache git

RUN apk add --no-cache \
	bash \
	curl \
	git \
	openssh \
  wget


ENV INSTALL_DIRECTORY /usr/local/bin
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
