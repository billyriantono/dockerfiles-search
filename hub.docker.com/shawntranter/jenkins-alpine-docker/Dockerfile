FROM jenkins/jenkins:lts-alpine

USER root
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk update
RUN apk add docker
