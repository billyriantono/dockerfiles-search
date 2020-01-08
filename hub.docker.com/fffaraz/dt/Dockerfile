FROM golang:alpine
MAINTAINER Faraz Fallahi <fffaraz@gmail.com>
ENTRYPOINT ["dt"]
RUN \
	apk add --update --no-cache git && \
	go get github.com/42wim/dt && \
	apk del git pcre expat libcurl libssh2 && \
	rm -rf /go/pkg /go/src /var/cache/apk/*
