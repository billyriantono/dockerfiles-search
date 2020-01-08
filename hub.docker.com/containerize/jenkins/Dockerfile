FROM jenkins/jenkins:lts-alpine
LABEL maintainer="llitfkitfk@gmail.com"

USER root
RUN apk add --no-cache docker
USER jenkins

# ENV DOCKER_HOST=unix:///var/run/docker.sock
ENV DOCKER_HOST=tcp://docker:2375