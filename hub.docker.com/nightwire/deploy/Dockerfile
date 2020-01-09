FROM alpine:latest
MAINTAINER Philip Henning <mail@philip-henning.com>

RUN apk add --update --no-cache ca-certificates openssl openssh-client rsync bash

COPY ./add-ssh-key.sh /add-ssh-key.sh

VOLUME /src
VOLUME /output

WORKDIR /src
