FROM ubuntu:18.04

ENV HUB_VERSION 2.7.0
ENV HELM_VERSION 2.12.1

# env subsets
RUN apt-get update && \
    apt-get install -y git wget

# hub (github cli)
RUN wget -O /tmp/hub-linux-amd64-$HUB_VERSION.tgz "https://github.com/github/hub/releases/download/v$HUB_VERSION/hub-linux-amd64-$HUB_VERSION.tgz" && \
    tar -C /tmp -zxf "/tmp/hub-linux-amd64-$HUB_VERSION.tgz" && \
    mv /tmp/hub-linux-amd64-$HUB_VERSION/bin/hub /usr/local/bin/ && \
    hub --version && \
    rm -rf /tmp/*

# helm
RUN wget -O /tmp/helm-v$HELM_VERSION-linux-amd64.tar.gz "https://storage.googleapis.com/kubernetes-helm/helm-v$HELM_VERSION-linux-amd64.tar.gz" && \
    tar -C /tmp -zxf "/tmp/helm-v$HELM_VERSION-linux-amd64.tar.gz" && \
    mv tmp/linux-amd64/helm /usr/local/bin/helm && \
    helm version --client && \
    rm -rf /tmp/*