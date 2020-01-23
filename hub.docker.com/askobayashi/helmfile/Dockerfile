# Based on https://www.github.com/anguswilliams/helmfile-docker

FROM alpine:3.9

ARG KUBECTL_VERSION=1.17.0

ARG HELM_VERSION=3.0.2
ARG HELM_SHA256="c6b7aa7e4ffc66e8abb4be328f71d48c643cb8f398d95c74d075cfb348710e1d"
ARG HELM_DIFF_VERSION=master
ARG HELM_SECRETS_VERSION=master

ARG HELMFILE_VERSION=0.98.2
ARG HELMFILE_SHA256="0e3000dc9689addabf6c880affc52566c84888802d79e523288cf3a6ec0e93d7"


LABEL version="${HELMFILE_VERSION}-${HELM_VERSION}-${KUBECTL_VERSION}"

WORKDIR /

RUN apk --update --no-cache add bash ca-certificates git curl

# kubectl
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/kubectl

# helmfile
ARG HELMFILE_LOCATION="https://github.com/roboll/helmfile/releases/download"
ARG HELMFILE_FILENAME="helmfile_linux_amd64"
RUN curl -LO ${HELMFILE_LOCATION}/v${HELMFILE_VERSION}/${HELMFILE_FILENAME} && \
    echo Verifying ${HELMFILE_FILENAME}... && \
    sha256sum ${HELMFILE_FILENAME} | grep -q "${HELMFILE_SHA256}" && \
    mv ${HELMFILE_FILENAME} /usr/local/bin/helmfile && \
    chmod +x /usr/local/bin/helmfile

# helm
ARG HELM_LOCATION="https://get.helm.sh"
ARG HELM_FILENAME="helm-v${HELM_VERSION}-linux-amd64.tar.gz"
RUN curl -LO ${HELM_LOCATION}/${HELM_FILENAME} && \
    echo Verifying ${HELM_FILENAME}... && \
    sha256sum ${HELM_FILENAME} | grep -q "${HELM_SHA256}" && \
    echo Extracting ${HELM_FILENAME}... && \
    tar zxvf ${HELM_FILENAME} && mv /linux-amd64/helm /usr/local/bin/ && \
    rm ${HELM_FILENAME} && rm -r /linux-amd64

ENV HELM_HOME=/etc/helm
ENV XDG_CACHE_HOME=${HELM_HOME}/.cache/helm \
    XDG_CONFIG_HOME=${HELM_HOME}/.config/helm \
    XDG_DATA_HOME=${HELM_HOME}/.local/share/helm

RUN mkdir -p ${HELM_HOME} ${XDG_CACHE_HOME} ${XDG_CONFIG_HOME} ${XDG_DATA_HOME} && \
    helm plugin install https://github.com/databus23/helm-diff --version ${HELM_DIFF_VERSION} && \
    helm plugin install https://github.com/futuresimple/helm-secrets --version ${HELM_SECRETS_VERSION}

ENV HELMFILE_HELM3="1"

ENTRYPOINT ["/usr/local/bin/helmfile"]

