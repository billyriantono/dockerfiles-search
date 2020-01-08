FROM jenkins/jenkins:lts

LABEL  maintainer="Richard Benko <benko.richard86@gmail.com>"

USER root

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    iptables \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sSL https://get.docker.com/ | sh \
    && usermod -aG docker jenkins

USER jenkins
