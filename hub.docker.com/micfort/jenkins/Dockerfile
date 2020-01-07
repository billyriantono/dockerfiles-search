# Use an official Python runtime as a parent image
FROM jenkins/jenkins:lts-alpine

USER root

RUN    delgroup ping \
    && addgroup -g 999 docker \
    && apk --no-cache add docker \
    && adduser jenkins docker

USER jenkins
