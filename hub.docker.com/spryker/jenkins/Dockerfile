FROM jenkins/jenkins:2.176.1-alpine

USER root

ENV JAVA_OPTS='-Djenkins.install.runSetupWizard=false -Xms128m -Xmx128m'

RUN apk update && \
    apk add \
    docker \
    shadow

USER jenkins
