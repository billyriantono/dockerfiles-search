FROM python:3.7-alpine3.8
LABEL maintainer="adam@grahamdigital.com"

RUN apk update; \
	apk upgrade; \
	apk add --update wget bash build-base tesseract-ocr-dev; \
	rm -rf /var/cache/apk/*

WORKDIR /opt/
RUN wget -O master.zip https://codeload.github.com/CCExtractor/ccextractor/zip/master; \
	unzip master.zip 'ccextractor-master/linux/*' -d /opt/; \
	unzip master.zip 'ccextractor-master/src/*' -d /opt/; \
	cd /opt/ccextractor-master/linux/; ./build; \
	cp ccextractor /usr/local/bin; \
	rm -rf /opt/*
