FROM ubuntu:16.04
MAINTAINER Elifarley <elifarley@gmail.com>
ENV \
  BASE_IMAGE=ubuntu:16.04

RUN apt-get update -y && apt-get install -y ca-certificates curl && \
  curl -fsSL https://raw.githubusercontent.com/elifarley/cross-installer/master/install.sh | sh && \
  xinstall save-image-info && \
  xinstall add jdk-6-nodesktop && \
  xinstall cleanup && \
  xinstall meta remove
