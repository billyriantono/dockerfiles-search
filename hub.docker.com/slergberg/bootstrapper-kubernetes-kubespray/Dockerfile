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
  && apk add --no-cache --virtual build-dependencies \
    curl \
    jq \
  && KUBECTL_VERSION=$(curl -SsL --retry 5 "https://storage.googleapis.com/${KUBEADM_SOURCE}/${KUBEADM_TRACK}") \
  && curl -SsL --retry 5 "https://storage.googleapis.com/${KUBEADM_SOURCE}/${KUBEADM_VERSION}/bin/${KUBEADM_ARCH}/kubeadm" > /usr/bin/kubeadm \
  && chmod +x /usr/bin/kubeadm \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*

# kubectl
ARG KUBECTL_SOURCE=kubernetes-release/release
ARG KUBECTL_TRACK=stable.txt
ARG KUBECTL_ARCH=linux/amd64
RUN set -ex \
  && apk add --no-cache --virtual build-dependencies \
    curl \
    jq \
  && KUBECTL_VERSION=$(curl -SsL --retry 5 "https://storage.googleapis.com/${KUBECTL_SOURCE}/${KUBECTL_TRACK}") \
  && curl -SsL --retry 5 "https://storage.googleapis.com/${KUBECTL_SOURCE}/${KUBECTL_VERSION}/bin/${KUBECTL_ARCH}/kubectl" > /usr/bin/kubectl \
  && chmod +x /usr/bin/kubectl \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*

# kustomize
RUN set -ex \
  && apk add --no-cache --virtual build-dependencies \
    curl \
    jq \
  && KUSTOMIZE_VERSION=$(curl -SsL --retry 5 "https://api.github.com/repos/kubernetes-sigs/kustomize/releases/latest" | jq --raw-output ".assets[] | select(.browser_download_url | contains (\"linux_amd64\")) | .browser_download_url") \
  && curl -SsL --retry 5 $KUSTOMIZE_VERSION > /usr/bin/kustomize \
  && chmod +x /usr/bin/kustomize \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*

# terraform
RUN set -ex \
  && apk add --no-cache --virtual build-dependencies \
    curl \
    jq \
  && TERRAFORM_VERSION=$(curl -SsL --retry 5 "https://checkpoint-api.hashicorp.com/v1/check/terraform" | jq --raw-output ".current_version") \
  && curl --output terraform.zip -SsL --retry 5 "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" \
  && unzip terraform.zip \
  && rm terraform.zip \
  && mv terraform /usr/bin/terraform \
  && chmod +x /usr/bin/terraform \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*

# kubespray
RUN set -ex \
  && apk add --no-cache --virtual build-dependencies \
    curl \
    gcc \
    git \
    jq \
    libffi-dev \
    make \
    musl-dev \
    openssl-dev \
  && KUBESPRAY_VERSION=$(curl -SsL --retry 5 "https://api.github.com/repos/kubernetes-sigs/kubespray/releases/latest" | jq --raw-output ".tag_name" | tr -d "v") \
  && curl --output kubespray.zip -SsL --retry 5 "https://github.com/kubernetes-sigs/kubespray/archive/v${KUBESPRAY_VERSION}.zip" \
  && unzip kubespray.zip \
  && rm kubespray.zip \
  && pip install -r "kubespray-${KUBESPRAY_VERSION}/requirements.txt" \
  && mkdir -p /kubespray \
  && mv "kubespray-${KUBESPRAY_VERSION}/cluster.yml" /kubespray/ \
  && mv "kubespray-${KUBESPRAY_VERSION}/contrib" /kubespray/contrib \
  && mv "kubespray-${KUBESPRAY_VERSION}/inventory/sample" /kubespray/inventory \
  && mv "kubespray-${KUBESPRAY_VERSION}/library" /kubespray/library \
  && mv "kubespray-${KUBESPRAY_VERSION}/remove-node.yml" /kubespray/ \
  && mv "kubespray-${KUBESPRAY_VERSION}/reset.yml" /kubespray/ \
  && mv "kubespray-${KUBESPRAY_VERSION}/roles" /kubespray/roles \
  && mv "kubespray-${KUBESPRAY_VERSION}/scale.yml" /kubespray/ \
  && mv "kubespray-${KUBESPRAY_VERSION}/scripts" /kubespray/scripts \
  && mv "kubespray-${KUBESPRAY_VERSION}/upgrade-cluster.yml" /kubespray/ \
  && rm -r "kubespray-${KUBESPRAY_VERSION}" \
  && apk del \
    build-dependencies \
  && rm -rf /var/cache/apk/*

# workdir
WORKDIR /application

# secrets
RUN mkdir /root/.ssh \
  && ln -s "/run/secrets/ssh_private_key" "/root/.ssh/id_rsa" \
  && ln -s "/run/secrets/ssh_public_key" "/root/.ssh/id_rsa.pub"
