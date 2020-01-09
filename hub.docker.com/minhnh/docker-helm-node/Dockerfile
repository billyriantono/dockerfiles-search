FROM node:7-slim
MAINTAINER Minh Nguyen-Hue "minh.nh1989@gmail.com"

ENV HELM_VERSION v2.4.2
RUN cd /tmp \
  && curl -L https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz -o helm-${HELM_VERSION}-linux-amd64.tar.gz \
  && tar -zxvf helm-${HELM_VERSION}-linux-amd64.tar.gz \
  && cp -a linux-amd64/helm /usr/local/bin \
  && chmod +x /usr/local/bin/helm \
  && rm -rf helm-${HELM_VERSION}-linux-amd64*

RUN \
  apt-get update \
  && apt-get install -y git python-virtualenv

RUN mkdir -p ~/.helm/plugins && helm plugin install https://github.com/technosophos/helm-template

WORKDIR /

CMD bash
