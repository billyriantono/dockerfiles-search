FROM travix/gocd-agent-gcloud:18.12.0

MAINTAINER Travix

# install packages
RUN (curl --silent --location https://deb.nodesource.com/setup_8.x | bash -) \
    && apt-get update \
    && apt-get install -y \
        aufs-tools \
        build-essential \
        nodejs \
        parallel \
    && apt-get clean \
    && node --version \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && npm install -g npm@6.7.0 \
    && npm install -g npm-cache@0.7.0