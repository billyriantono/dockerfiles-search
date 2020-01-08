FROM alpine:latest

RUN apk add python3

RUN apk add --no-cache --virtual .build-deps \
	python3-dev \
	gcc \
	musl-dev \
	linux-headers \
	libffi-dev \
	openssl-dev \
    && pip3 install openstacksdk \
    O365 \
    && apk del .build-deps
