FROM alpine

ARG helm_version=v3.0.0
ARG helm_os=linux
ARG helm_arch=amd64

RUN set -eu \
  && wget https://get.helm.sh/helm-$helm_version-$helm_os-$helm_arch.tar.gz -O /tmp/helm.tar.gz \
  && mkdir /opt/helm \
  && cd /opt/helm \
  && tar xzf /tmp/helm.tar.gz \
  && rm /tmp/helm.tar.gz \
  && ln -s /opt/helm/$helm_os-$helm_arch/helm /usr/local/bin/
