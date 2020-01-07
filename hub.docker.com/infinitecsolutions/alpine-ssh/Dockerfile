FROM alpine:latest

LABEL maintainer="https://github.com/keklikhasan"

ENV ROOT_PASSWORD root

RUN apk update	&& apk upgrade && apk add openssh \
		&& rm -rf /var/cache/apk/* /tmp/*

RUN mkdir ~/.ssh