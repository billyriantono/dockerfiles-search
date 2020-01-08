
FROM docker:latest
LABEL MAINTAINER="Jeshan BABOOA <j@jeshan.co>"

RUN apk add --no-cache curl py-pip
RUN pip install docker-compose

ENV MACHINE_VERSION=0.12.2 COMPOSE_VERSION=1.15.0

WORKDIR /usr/local/bin
RUN curl -L "https://github.com/docker/machine/releases/download/v${MACHINE_VERSION}/docker-machine-Linux-x86_64" \
  -o docker-machine && chmod +x docker-machine

RUN cd /usr/local/bin/ && rm -rf dockerd docker-containerd docker-containerd-ctr docker-runc \
  docker-containerd-shim docker-proxy docker-init
