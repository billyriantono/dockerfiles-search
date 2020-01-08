FROM jenkins/jenkins:alpine

USER root
RUN apk update && \
    apk add docker
USER jenkins

VOLUME /var/run/docker.sock
