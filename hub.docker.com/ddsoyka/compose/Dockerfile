FROM debian:latest

LABEL maintainer="ddsoyka@deprecatedlogic.ca"

ENV INSTALLATION_PATH /usr/local/bin/docker-compose
ENV DOCKER_COMPOSE_VERSION 1.24.0

VOLUME ~/.ssh

RUN apt update && \
    apt --no-install-recommends --yes install \
    curl \
    git \
    openssh-client \
    gpg-agent \
    gnupg2 \
    apt-transport-https \
    ca-certificates \
    software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable"
RUN apt update && \
    apt --no-install-recommends --yes install \
    docker-ce \
    docker-ce-cli \
    containerd.io
RUN curl -L "https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" > /tmp/docker-compose && \
    chmod +x /tmp/docker-compose && \
    mv /tmp/docker-compose $INSTALLATION_PATH

HEALTHCHECK CMD docker-compose version | grep -Fxq $DOCKER_COMPOSE_VERSION

ENTRYPOINT [ "docker-compose" ]