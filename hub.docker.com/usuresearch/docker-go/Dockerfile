FROM golang:1.13-alpine

LABEL maintainer="USU Software AG"

RUN apk update && apk add git gcc musl-dev bash

CMD ["/bin/bash"]

ENV HOME /root
WORKDIR /root
