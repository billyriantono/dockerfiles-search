FROM ubuntu:xenial
MAINTAINER ""

ENV TERRAFORM_VERSION=0.11.2

RUN apt-get update && apt-get install -y git unzip wget awscli \
  && mkdir /data
WORKDIR /data
RUN mkdir /data/bin \
  && wget -q https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -O /data/bin/terraform.zip \
  && unzip /data/bin/terraform.zip -d /data/bin \
  && rm -rf /data/bin/terraform.zip
COPY bin/* /data/bin/
RUN chmod +x /data/bin/*
ENV PATH="/data/bin:${PATH}"
