FROM alpine:latest

LABEL Edin Ćoralić <edin.coralic@cartargetgroup.com>

RUN \
	apk update && \
	apk upgrade && \
	apk add git openssh bash apache2-utils curl && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

WORKDIR /do
