# Base image
FROM python:3.7-alpine

# AWS CLI
RUN pip install --upgrade \
  awscli

# kubeadm
ARG KUBEADM_SOURCE=kubernetes-release/release
ARG KUBEADM_TRACK=stable.txt
ARG KUBEADM_ARCH=linux/amd64
RUN set -ex \
  && apk add --no-cache \
    curl \
    jq \
  && KUBECTL_VERSION=$(curl -SsL --retry 5 "https://storage.googleapis.com/${KUBEADM_SOURCE}/${KUBEADM_TRACK}") \
  && curl -SsL --retry 5 "https://storage.googleapis.com/${KUBEADM_SOURCE}/${KUBEADM_VERSION}/bin/${KUBEADM_ARCH}/kubeadm" > /usr/bin/kubeadm \
  && chmod +x /usr/bin/kubeadm \
  && apk del \
    curl \
    jq \
  && rm -rf /var/cache/apk/*

# kubectl
ARG KUBECTL_SOURCE=kubernetes-release/release
ARG KUBECTL_TRACK=stable.txt
ARG KUBECTL_ARCH=linux/amd64
RUN set -ex \
  && apk add --no-cache \
    curl \
    jq \
  && KUBECTL_VERSION=$(curl -SsL --retry 5 "https://storage.googleapis.com/${KUBECTL_SOURCE}/${KUBECTL_TRACK}") \
  && curl -SsL --retry 5 "https://storage.googleapis.com/${KUBECTL_SOURCE}/${KUBECTL_VERSION}/bin/${KUBECTL_ARCH}/kubectl" > /usr/bin/kubectl \
  && chmod +x /usr/bin/kubectl \
  && apk del \
    curl \
    jq \
  && rm -rf /var/cache/apk/*

# kustomize
RUN set -ex \
  && apk add --no-cache \
    curl \
    jq \
  && KUSTOMIZE_VERSION=$(curl -SsL --retry 5 "https://api.github.com/repos/kubernetes-sigs/kustomize/releases/latest" | jq --raw-output ".assets[] | select(.browser_download_url | contains (\"linux_amd64\")) | .browser_download_url") \
  && curl -SsL --retry 5 $KUSTOMIZE_VERSION > /usr/bin/kustomize \
  && chmod +x /usr/bin/kustomize \
  && apk del \
    curl \
    jq \
  && rm -rf /var/cache/apk/*

# kops
ARG GO_VERSION=1.8.1
ARG KOPS_GITISH=release
RUN set -ex \
  && apk add --no-cache --virtual build-dependencies \
    bash \
    curl \
    gcc \
    git \
    go \
    jq \
    make \
    musl-dev \
    openssl \
  && apk add --no-cache \
    ca-certificates \
    vim \
  && export GOROOT_BOOTSTRAP="$(go env GOROOT)" \
  && curl -L https://golang.org/dl/go${GO_VERSION}.src.tar.gz | tar zx -C /usr/local \
  && cd /usr/local/go/src \
  && ./make.bash \
  && mkdir -p /go \
  && export GOPATH=/go \
  && go get -d k8s.io/kops \
  && cd ${GOPATH}/src/k8s.io/kops/ \
  && git checkout ${KOPS_GITISH} \
  && make SHASUMCMD=0 \
  && mv ${GOPATH}/bin/kops /usr/bin/. \
  && rm -rf /go /usr/local/go \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*
