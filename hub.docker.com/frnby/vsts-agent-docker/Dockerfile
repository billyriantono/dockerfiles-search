FROM microsoft/vsts-agent:ubuntu-16.04-tfs-2018-docker-17.12.0-ce

ENV DOCKER_COMPOSE_VERSION 1.22.0

RUN set -x \
 && curl -fSL "https://github.com/docker/compose/releases/download/$DOCKER_COMPOSE_VERSION/docker-compose-`uname -s`-`uname -m`" -o /usr/local/bin/docker-compose \
 && chmod +x /usr/local/bin/docker-compose \
 && docker-compose -v
