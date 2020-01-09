FROM alpine:3.9
ENV TERRAFORM_VERSION=0.11.14
RUN apk update && \
    apk add curl jq python bash ca-certificates git openssl unzip wget py2-pip && \
    pip install --upgrade awscli && \
    cd /tmp && \
    wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/bin && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/* && \
    rm -rf /var/tmp/*
