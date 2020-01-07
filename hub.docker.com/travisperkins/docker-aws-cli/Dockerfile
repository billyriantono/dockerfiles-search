FROM docker:17.06.2

ENV AWS_CLI_VERSION 1.11.171

RUN apk add --update python py-pip jq && \
    pip install --upgrade awscli==${AWS_CLI_VERSION} && \
    apk del py-pip && \
    rm -rf /var/cache/apk/*
