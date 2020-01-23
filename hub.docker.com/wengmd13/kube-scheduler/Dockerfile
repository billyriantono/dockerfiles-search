FROM alpine:3.5

MAINTAINER We ahead <docker@weahead.se>

RUN apk update && apk add ca-certificates && update-ca-certificates && apk add openssl

WORKDIR /usr/bin/

ENV COMPOSE_VERSION=0.12.0

RUN wget  \
      https://releases.rancher.com/compose/v${COMPOSE_VERSION}/rancher-compose-linux-amd64-v${COMPOSE_VERSION}.tar.gz \
      && tar --strip-components=1 -xvzf rancher-compose-linux-amd64-v${COMPOSE_VERSION}.tar.gz \
      && mv ./rancher-compose-v${COMPOSE_VERSION}/rancher-compose . \
      && rm rancher-compose-linux-amd64-v0.12.0.tar.gz \
      && rm -r ./rancher-compose-v${COMPOSE_VERSION}

RUN mkdir /data

WORKDIR /data

ENTRYPOINT [ "/usr/bin/rancher-compose" ]
