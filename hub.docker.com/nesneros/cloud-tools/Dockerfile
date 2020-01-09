FROM ubuntu:16.10

RUN apt-get update \
&& apt-get install -y apt-transport-https apt-utils curl emacs git lsb-release openssh-server python ssh sudo zsh

ENV GCLOUD_VERSION=151.0.1

RUN curl -sSL --fail https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-$GCLOUD_VERSION-linux-x86_64.tar.gz | tar zxf -
RUN cd /google-cloud-sdk && ./install.sh --additional-components kubectl beta

