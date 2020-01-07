FROM alpine

LABEL maintainer="Yannick Foeillet <bzhtux@gmail.com>"

RUN apk add --no-cache \
    bash \
    curl \
    jq

RUN curl -L "https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl \
    && curl -L "https://get.helm.sh/helm-v2.15.0-linux-amd64.tar.gz" -o /tmp/helm.tgz \
    && tar xvf /tmp/helm.tgz -C /tmp \
    && mv /tmp/linux-amd64/helm /usr/local/bin/ \
    && mv /tmp/linux-amd64/tiller /usr/local/bin/ \
    && rm -rf /tmp/linux-amd64 
