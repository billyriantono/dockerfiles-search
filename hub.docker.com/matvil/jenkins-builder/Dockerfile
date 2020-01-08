FROM jenkins/jnlp-slave:3.19-1

USER root

# Required packages
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        git make python-setuptools curl ca-certificates && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install aws-cli
RUN easy_install awscli

# Install Docker
ENV DOCKER_RELEASE=18.09.2
RUN curl -L https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_RELEASE}.tgz -o - | \
        tar -C /opt -xz docker/docker && \
    ln -s /opt/docker/docker /usr/local/bin

# Install docker-compose
ENV DOCKER_COMPOSE_VERSION=1.21.0
RUN curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m) \
        -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

USER jenkins
