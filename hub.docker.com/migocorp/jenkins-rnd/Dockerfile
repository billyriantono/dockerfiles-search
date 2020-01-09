FROM jenkins/jenkins:lts
LABEL maintainer="Larry SU <larry_su@migocorp.com>"

USER root

RUN apt-get update \
    && apt-get -y --no-install-recommends install vim \
    && apt-get -y --no-install-recommends install netcat \
    && apt-get -y --no-install-recommends install net-tools

USER jenkins
