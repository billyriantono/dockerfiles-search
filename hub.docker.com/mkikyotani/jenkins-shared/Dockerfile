FROM frolvlad/alpine-glibc:alpine-3.8
MAINTAINER Deloitte Mitsufumi Kikyotani 
LABEL BASE_IMAGE="alpine:3.8" \
      VERSION="1.0" \
      TOOLS="git, oc_v3.11" \
      DESCRIPTION="This image will be used for common purposes across projects"

USER root

COPY . /tmp/ 


RUN \
    apk add --update ca-certificates wget git && \
    wget -q -O /tmp/openshift-client.tar.gz \
    https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz && \
    tar -xvf /tmp/openshift-client.tar.gz --strip-components 1 -C /tmp && \
    mv -v /tmp/oc /bin && \
    rm -rfv /tmp/* /var/cache/apk/*

CMD ["echo", "Running..."]

