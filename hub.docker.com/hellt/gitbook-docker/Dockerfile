FROM node:6-alpine

MAINTAINER Roman Dodin <dodin.roman@gmail.com>

RUN npm install --global gitbook-cli &&\
	gitbook fetch latest &&\
	npm cache clear &&\
	rm -rf /tmp/*

WORKDIR /srv/gitbook
