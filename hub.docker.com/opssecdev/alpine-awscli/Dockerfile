FROM alpine:latest

COPY cli-version /

RUN \
##  apk --no-cache update && \
    apk --no-cache -u add \
        python \
        py-pip \
        py-setuptools \
        ca-certificates \
        groff \
        less \
        jq && \
    pip --no-cache-dir install \
        aws-shell \
        awsebcli \
        awscli==$(cat /cli-version) && \
##  apk --purge -v del py-pip && \
    rm -rf /var/cache/apk/*

VOLUME /root/.aws
WORKDIR /work
