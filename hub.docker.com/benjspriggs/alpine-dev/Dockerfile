FROM alpine:latest

RUN apk add --update \
	sudo \
	&& rm -rf /var/cache/apk/*

RUN adduser -D dev
RUN echo 'dev:dev' | chpasswd
RUN echo 'dev ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER dev
