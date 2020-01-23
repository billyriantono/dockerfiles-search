FROM jenkins/jenkins:lts
MAINTAINER Andrey Romanov <ansromanov@gmail.com>

# Suppress apt installation warnings
ENV DEBIAN_FRONTEND=noninteractive

# Change to root user
USER root

# Used to set the docker group ID
# Set to 497 by default, which is the group ID used by AWS Linus ECS Instance
ARG DOCKER_GID=497

# Create Docker Group with GID
# Set default value of 497 if DOCKER_GID set to blank string by Docker Compose
RUN groupadd -g ${DOCKER_GID:-497} docker

# Used to control docker and docker compose versions installed
# ARG DOCKER_ENGINE=1.13.0
# ARG DOCKER_COMPOSE=1.17.0

# Install base packages
RUN apt-get update -y && \
  apt-get install apt-transport-https curl python-dev python-setuptools gcc make libssl-dev -y && \
  easy_install pip

# Install Docker 
RUN apt-get update -y && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

RUN curl -fsSLO https://download.docker.com/linux/ubuntu/gpg && \
    apt-key add gpg && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable" && \
    apt-get update -y && \
    apt-get install -y docker-ce

# Install Docker Compose
RUN curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose && \
  chmod +x /usr/local/bin/docker-compose && \
  curl -L https://raw.githubusercontent.com/docker/compose/1.17.0/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose

# Change to jenkins user
USER jenkins

# Add Jenkins plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# password 91b2eba5a63a42c2a2f0d9cfac1739ff