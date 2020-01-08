FROM alpine:3.6
MAINTAINER custa "custa@126.com"
ENV REFRESHED_AT 2017-04-21
RUN apk update && \
	apk add python3 && \
	apk add alpine-sdk python3-dev libffi-dev openssl-dev && \
	pip3 install ansible==2.4.0.0 && \
	apk del alpine-sdk python3-dev libffi-dev openssl-dev && \
	rm -rf /var/cache/apk/*
