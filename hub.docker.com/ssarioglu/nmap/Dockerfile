#A simple dockerfile for nmap
FROM alpine:latest
MAINTAINER Serdar.Sarioglu@mysystem.org

RUN apk update && apk add \
	nmap \
	nmap-scripts \
      	nmap-doc \
     	nmap-nping \
      	nmap-ncat \
	zmap \
	busybox \
	&& rm -rf /var/cache/apk/*

ENTRYPOINT ["nmap"]
