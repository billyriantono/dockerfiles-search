FROM alpine:3.7
MAINTAINER Bitbucket Pipelines

#ARG VERSION
#ENV AWS_CLI_VERSION

RUN apk --update --no-cache add \
    python \
    py-pip \
    jq \
    bash \
    git \
    groff \
    less \
    mailcap \
    bash \
    ca-certificates \
    curl \
    py-setuptools \
    rsync \
    openssh \
    && pip install --no-cache-dir awscli \
    && apk del py-pip \
    && rm -rf /var/cache/apk/* /root/.cache/pip/*

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT [ "aws" ]
CMD ["--version"]