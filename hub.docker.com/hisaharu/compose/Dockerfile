FROM docker:latest
ENV COMPOSE_VERSION 1.10.0
RUN wget -O /usr/local/bin/docker-compose https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m`
RUN chmod +x /usr/local/bin/docker-compose
