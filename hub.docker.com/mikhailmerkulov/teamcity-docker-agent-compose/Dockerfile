FROM jetbrains/teamcity-agent

LABEL maintainer "Mikhail Merkulov <mikhail.m@itomy.ch>"

ENV COMPOSE_VERSION 1.21.0

RUN curl -L https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-Linux-x86_64 > /usr/local/bin/docker-compose \
 && chmod +x /usr/local/bin/docker-compose