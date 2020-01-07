FROM golang:1-alpine

RUN apk add --no-cache \
		curl  \
		gcc \
		musl-dev \
		openssl \
		git
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
