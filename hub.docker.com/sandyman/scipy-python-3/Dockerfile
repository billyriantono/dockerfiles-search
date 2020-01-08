FROM alpine:3.10
MAINTAINER Sander Huijsen <sander.huijsen@gmail.com>

WORKDIR /build
ADD Dockerfile /build/

RUN apk update && apk add --no-cache bash python3
RUN apk add --virtual build-dependencies build-base gcc python3-dev
RUN apk add openblas openblas-dev --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/community/ --allow-untrusted
RUN pip3 install --upgrade pip
RUN pip3 install numpy==1.17.2 scipy==1.3.1
RUN apk del build-dependencies
