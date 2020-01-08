FROM debian:stretch-slim

COPY ./bitbucket-notify /bitbucket-notify
COPY ./chart-deploy /chart-deploy

RUN apt update \
    && apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    && curl -sL https://deb.nodesource.com/setup_11.x | bash - \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable" \
    && curl -o /tmp/helm.tar.gz https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-amd64.tar.gz \
    && cd /tmp/ && tar -zxvf /tmp/helm.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl \
    && curl -Lo /tmp/rancher.tar.gz https://releases.rancher.com/cli2/v2.0.6/rancher-linux-amd64-v2.0.6.tar.gz \
    && tar -zxvf /tmp/rancher.tar.gz \
    && mv rancher-v2.0.6/rancher /usr/local/bin/rancher \
    && apt-get update && apt-get install -y --allow-unauthenticated \
    python \
    make \
    gcc \
    nodejs \
    yarn \
    docker-ce \
    bzip2 \
    phantomjs \
    git \
    openssh-client \
    build-essential \
    checkinstall \
    && cd /bitbucket-notify \
    && yarn install \
    && echo "node /bitbucket-notify/bitbucket-notify.js \$@" > /usr/local/bin/bitbucket-notify \
    && chmod +x /usr/local/bin/bitbucket-notify \
    && echo "node /bitbucket-notify/sync-branches.js \$@" > /usr/local/bin/sync-branches \
    && chmod +x /usr/local/bin/sync-branches \
    && cd /chart-deploy \
    && yarn install \
    && echo "node /chart-deploy/index.js \$@" > /usr/local/bin/chart-deploy \
    && chmod +x /usr/local/bin/chart-deploy \
    && export SUDO_FORCE_REMOVE=yes \
    && rm -rf /tmp/* \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false;

# test
RUN nodejs -v \
    && npm -v \
    && yarn -v \
    && docker -v \
    && bitbucket-notify -v \
    && sync-branches -v \
    && helm version -c \
    && kubectl version --client \
    && chart-deploy -v \
    && rancher -v
