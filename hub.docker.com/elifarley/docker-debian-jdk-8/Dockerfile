FROM debian:jessie-slim
MAINTAINER Elifarley Cruz <elifarley@gmail.com>
ENV \
  BASE_IMAGE=debian:jessie-slim

RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates curl && \
  curl -fsSL https://raw.githubusercontent.com/elifarley/cross-installer/master/install.sh | sh && \
  xinstall save-image-info && \
  xinstall add jdk-8-nodesktop && \
  xinstall cleanup && \
  xinstall meta remove
