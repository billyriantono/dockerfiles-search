FROM node:10.16.3
MAINTAINER R3 Interworks, Inc.

# Update the things
RUN apt-get update \
    && apt-get install -y \
        software-properties-common \
        build-essential \
        wget \
        xvfb \
        curl \
        git \
        ssh-client \
        unzip \
        iputils-ping \
    && rm -rf /var/lib/apt/lists/*

# Update npm
RUN npm install -g npm

# Install Build Dependencies
RUN npm install -g gulp webpack webpack-cli --no-audit

# Set up bitbucket env/user
RUN mkdir -p /opt/atlassian/bitbucketci/agent/build \
    && sed -i '/[ -z \"PS1\" ] && return/a\\ncase $- in\n*i*) ;;\n*) return;;\nesac' /root/.bashrc \
    && useradd --create-home --shell /bin/bash --uid 1001 pipelines

WORKDIR /opt/atlassian/bitbucketci/agent/build
ENTRYPOINT /bin/bash
