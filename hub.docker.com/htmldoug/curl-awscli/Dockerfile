FROM alpine:3.2

RUN \
	mkdir -p /aws && \
	apk --update-cache --verbose add curl python py-pip && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*

WORKDIR /aws
