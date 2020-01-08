FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl jq
RUN curl -L https://github.com/openshift/origin/releases/download/v1.5.0/openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit.tar.gz | tar zx && \
    mv openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit/oc /usr/bin/ && \
    rm -rf openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit && oc version

