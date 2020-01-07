FROM alpine:latest
MAINTAINER polandj

RUN apk --no-cache upgrade --update

RUN apk --no-cache add make

RUN apk --no-cache add python py-pip py-setuptools ca-certificates curl groff less 
RUN pip --no-cache-dir install --upgrade pip awscli

RUN apk --no-cache add npm

