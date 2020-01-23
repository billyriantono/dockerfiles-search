# Go lang image
FROM astau/alpine:latest

MAINTAINER Srikanth <srikanth@astau.com>

RUN apk add go \
	&& rm -rf /var/cache/apk/*

ENV GO_HOME /usr/lib/go
ENV PATH $PATH:$GO_HOME/bin

CMD ["go", "version"]