FROM alpine:3.1
MAINTAINER Carles Amigó, fr3nd@fr3nd.net

RUN apk --update add git python py-pip

ENV DOCKERCOMPOSE_VERSION 1.4.0

RUN pip install -e git+https://github.com/docker/compose.git@$DOCKERCOMPOSE_VERSION#egg=docker-compose

RUN mkdir -p /workspace
WORKDIR /workspace

ENTRYPOINT [ "/usr/bin/docker-compose" ]
