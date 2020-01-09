FROM docker:dind
ARG COMPOSE_VERSION=1.24.1
ADD \
  https://github.com/docker/compose/releases/download/$COMPOSE_VERSION/run.sh \
  /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
