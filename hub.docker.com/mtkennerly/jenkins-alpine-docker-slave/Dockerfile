FROM jenkins/slave:alpine

USER root

RUN apk update && apk add docker openrc

RUN rc-update add docker boot

USER jenkins
