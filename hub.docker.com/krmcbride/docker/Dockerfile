FROM docker:17.03.1-git

RUN apk add --no-cache \
        bash \
        curl \
        py-pip

ENV DOCKER_COMPOSE_VERSION 1.13.0
RUN pip install 'docker-compose=='${DOCKER_COMPOSE_VERSION}
