FROM alpine:latest
MAINTAINER Jason Wilder <mail@jasonwilder.com>

RUN apk -U add openssl

ENV VERSION 0.7.3
ENV DOWNLOAD_URL https://github.com/exira/docker-gen/releases/download/$VERSION/docker-gen-alpine-linux-amd64-$VERSION.tar.gz
ENV DOCKER_HOST unix:///tmp/docker.sock

RUN wget -qO- $DOWNLOAD_URL | tar xvz -C /usr/local/bin

RUN mkdir -p /etc/docker-gen/templates/ && \
    wget -q -O /etc/docker-gen/templates/sniproxy.tmpl https://raw.githubusercontent.com/exira/docker-gen/master/templates/sniproxy.tmpl

ENTRYPOINT ["/usr/local/bin/docker-gen"]
