FROM alpine:latest

MAINTAINER AND Digital <hello@and.digital>

ARG RANCHER_COMPOSE_VERSION=0.12.5
ARG RANCHER_COMPOSE_BINARY_URL=https://github.com/rancher/rancher-compose/releases/download/v${RANCHER_COMPOSE_VERSION}/rancher-compose-linux-amd64-v${RANCHER_COMPOSE_VERSION}.tar.gz

RUN apk add --update --quiet curl tar && \
	curl -sSL ${RANCHER_COMPOSE_BINARY_URL} | tar -xzp -C /usr/local/bin/ --strip-components=2 && \
	rm -rf /var/cache/*
