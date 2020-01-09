FROM ubuntu:16.04

LABEL version="1" \
  maintainer="Quizlet, Inc." \
  maintainer.email="android-engineering@quizlet.com" \
  description="Android build Docker image with support for gcloud" \
  repository="https://github.com/quizlet/docker-ftl"

# Set up dependencies & Java
RUN apt-get update \
  && apt-get install git --yes \
  && apt-get clean

# Set up gcloud
RUN apt-get update \
  && apt-get install curl apt-transport-https -y \
  && echo "deb https://packages.cloud.google.com/apt cloud-sdk-xenial main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
  && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
  && apt-get update \
  && apt-get install google-cloud-sdk -y \
  && apt-get clean

WORKDIR /tmp/project
