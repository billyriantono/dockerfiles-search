FROM alpine:3.4
MAINTAINER Mark Wienk <mark@wienkit.nl>

# Define rancher compose version
ENV RANCHER_COMPOSE_VERSION v0.12.5
ENV RANCHER_VERSION v0.6.13
# Download and install rancher compose
RUN apk add --no-cache --virtual .persistent-deps \
		ca-certificates \
		wget \
		tar \
		xz \
	&& wget -O /tmp/rancher-compose-linux-amd64-${RANCHER_COMPOSE_VERSION}.tar.gz "https://github.com/rancher/rancher-compose/releases/download/${RANCHER_COMPOSE_VERSION}/rancher-compose-linux-amd64-${RANCHER_COMPOSE_VERSION}.tar.gz" \
	&& tar -xf /tmp/rancher-compose-linux-amd64-${RANCHER_COMPOSE_VERSION}.tar.gz -C /tmp \
	&& mv /tmp/rancher-compose-${RANCHER_COMPOSE_VERSION}/rancher-compose /usr/local/bin/rancher-compose \
	&& rm -R /tmp/rancher-compose-linux-amd64-${RANCHER_COMPOSE_VERSION}.tar.gz /tmp/rancher-compose-${RANCHER_COMPOSE_VERSION}\
	&& chmod +x /usr/local/bin/rancher-compose

RUN wget -O /tmp/rancher-linux-amd64-${RANCHER_VERSION}.tar.gz "https://github.com/rancher/cli/releases/download/${RANCHER_VERSION}/rancher-linux-amd64-${RANCHER_VERSION}.tar.gz" \
    && tar -xf /tmp/rancher-linux-amd64-${RANCHER_VERSION}.tar.gz -C /tmp \
    && mv /tmp/rancher-${RANCHER_VERSION}/rancher /usr/local/bin/rancher \
    && rm -R /tmp/rancher-linux-amd64-${RANCHER_VERSION}.tar.gz /tmp/rancher-${RANCHER_VERSION} \
    && chmod +x /usr/local/bin/rancher

CMD ["rancher-compose"]
