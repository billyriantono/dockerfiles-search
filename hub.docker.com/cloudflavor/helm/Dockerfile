FROM alpine:latest

ARG HELM_VERSION=v2.11.0

ENV HELM_VERSION=$HELM_VERSION

WORKDIR /tmp

RUN wget https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    tar -xvf helm-${HELM_VERSION}-linux-amd64.tar.gz linux-amd64/helm --strip-components=1 -C /usr/local/bin/ && \
    rm -rf helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    mkdir -p /tmp/user && \
    chown 10001:10001 -R /tmp/user && \
    apk add --no-cache bash

WORKDIR /tmp/user

USER 10001

CMD ["/usr/local/bin/helm"]
