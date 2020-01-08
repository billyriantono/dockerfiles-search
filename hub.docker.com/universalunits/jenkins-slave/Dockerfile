FROM jenkins/jnlp-slave

ARG DOCKER_VERSION=18.06.3~ce~3-0~debian
ARG DOCKER_COMPOSE_VERSION=1.24.0
# 497 - id of docker group on AWS ECS
ARG DOCKER_SOCKET_GID=497

USER root
RUN apt update \
    && apt install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common \
    && curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg \
     | apt-key add - \
    && add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
     $(lsb_release -cs) \
     stable" \
    && apt update \
    && apt install -y docker-ce=${DOCKER_VERSION} \
    && usermod -aG docker jenkins \
    && curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

RUN echo 'deb http://http.debian.net/debian wheezy-backports main' > /etc/apt/sources.list.d/wheezy-backports-main.list \
    && curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash \
    && apt-get install git-lfs

RUN [ -n "$(getent group ${DOCKER_SOCKET_GID} | cut -d: -f1)" ] || groupadd -g $DOCKER_SOCKET_GID docker_socket; \
    usermod -aG ${DOCKER_SOCKET_GID} jenkins

RUN cd /tmp \
    && curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl \
    && curl -O https://amazon-eks.s3-us-west-2.amazonaws.com/1.11.5/2018-12-06/bin/linux/amd64/aws-iam-authenticator \
    && chmod +x ./aws-iam-authenticator \
    && mv ./aws-iam-authenticator /usr/local/bin/aws-iam-authenticator \
    && curl -LO https://storage.googleapis.com/kubernetes-helm/helm-v2.12.1-linux-amd64.tar.gz \
    && tar xzf helm-v2.12.1-linux-amd64.tar.gz \
    && mv ./linux-amd64/helm /usr/local/bin/helm \
    && rm -rf helm-v2.12.1-linux-amd64.tar.gz ./linux-amd64/helm \
    && runuser -l jenkins -c 'helm init --client-only'

USER jenkins

RUN mkdir /home/jenkins/workspace
