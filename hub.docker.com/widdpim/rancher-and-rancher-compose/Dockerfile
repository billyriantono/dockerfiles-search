# Set base image.
FROM alpine:latest

MAINTAINER Pim Widdershoven <pim@widdershoven.nl>

# Define rancher-compose version
ENV RANCHER_COMPOSE_VERSION=v0.12.5

# Define rancher version
ENV RANCHER_CLI_VERSION=v0.6.2

# Install dependencies, rancher and rancher-compose
RUN apk add --quiet --no-cache ca-certificates curl unzip && \
        apk add --quiet --no-cache --virtual build-dependencies && \
	curl -sSL "https://github.com/rancher/rancher-compose/releases/download/${RANCHER_COMPOSE_VERSION}/rancher-compose-linux-amd64-${RANCHER_COMPOSE_VERSION}.tar.gz" | tar -xzp -C /usr/local/bin/ --strip-components=2 && \
	curl -sSL "https://github.com/rancher/cli/releases/download/${RANCHER_CLI_VERSION}/rancher-linux-amd64-${RANCHER_CLI_VERSION}.tar.gz" | tar -xz -C /usr/local/bin/ --strip-components=2 && \
	chmod +x /usr/local/bin/rancher && \
	apk del build-dependencies && \
	rm -rf /var/cache/*

# Set working directory
WORKDIR /workspace

# Executing defaults
CMD ["/bin/sh"]
