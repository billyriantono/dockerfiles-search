FROM golang:alpine
MAINTAINER "Hibri Marzook <hibri@hibri.net>"

ENV TERRAFORM_VERSION=0.12.6

RUN apk add --update git bash openssh

ENV TF_DEV=true
ENV TF_RELEASE=true

WORKDIR $GOPATH/src/github.com/hashicorp/terraform
RUN git clone https://github.com/hashicorp/terraform.git ./ && \
    git checkout tags/v${TERRAFORM_VERSION}  -b v${TERRAFORM_VERSION} && \
    /bin/bash scripts/build.sh

RUN \
  apk update && \
  apk add bash py-pip && \
  apk add --virtual=build gcc libffi-dev musl-dev openssl-dev python-dev make && \
  pip --no-cache-dir install -U pip && \
  pip --no-cache-dir install azure-cli && \
  apk del --purge build
 
RUN az --version

WORKDIR $GOPATH
ENTRYPOINT ["terraform"]
