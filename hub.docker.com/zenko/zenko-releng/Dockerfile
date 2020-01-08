FROM docker:17.09.0-ce-git

ENV HELM_VER 2.11.0
ENV KUBECTL_VER 1.11.6
ENV ANSIBLE_VER 2.4.3
ENV BUILDBOT_VER 0.9.12

ENV GOPATH /go
RUN apk -U add --no-cache nodejs nodejs-npm make jq wget ca-certificates alpine-sdk python-dev libffi-dev openssl-dev py2-pip go curl curl-dev gettext && \
    npm install -g @commitlint/cli @commitlint/config-conventional conventional-commits-parser semver && \
    go get -u github.com/aktau/github-release && \
    wget -q https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VER}-linux-amd64.tar.gz && \
    tar -xvf helm-v${HELM_VER}-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/ && \
    wget -q https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VER}/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl && \
    pip install ansible==${ANSIBLE_VER} && \
    pip install buildbot-worker==${BUILDBOT_VER} && \
    apk del alpine-sdk python-dev libffi-dev openssl-dev

ENV PATH $GOPATH/bin:$PATH

ENV RUN_DOCKER=0
ARG WORKDIR=/workdir
RUN mkdir -p "${WORKDIR}"
WORKDIR /workdir
