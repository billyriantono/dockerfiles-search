FROM alpine:3.9

RUN apk add --update \
	git nodejs npm \
	&& npm install -g bower grunt-cli \
	&& rm -rf /var/cache/apk/*
