FROM jenkins/jenkins:2.138.1-alpine

USER root

ARG ARG_DOCKER_GROUP_ID=999
ENV DOCKER_GROUP_ID=${ARG_DOCKER_GROUP_ID}

ARG ARG_DOCKER_VERSION=18.06.1
ENV DOCKER_VERSION=${ARG_DOCKER_VERSION}

RUN apk --no-cache add shadow && usermod -aG ${DOCKER_GROUP_ID} jenkins

RUN wget https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}-ce.tgz && \
    tar xzvf  docker-18.06.1-ce.tgz && \
    mv docker/* /usr/bin/ && \
    rm docker-18.06.1-ce.tgz 

USER jenkins