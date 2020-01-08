FROM jenkins:2.0-alpine

USER root
RUN curl -sSL https://get.docker.com/builds/Linux/x86_64/docker-1.11.1.tgz | tar -xzv docker/docker && \
    mv docker/docker /usr/local/bin/ && \
    rmdir docker

RUN addgroup -g 999 docker && addgroup jenkins docker
USER jenkins
