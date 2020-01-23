FROM maven:3.5-jdk-8-slim

ARG GCLOUD_SDK_URL=https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-233.0.0-linux-x86_64.tar.gz

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/google-cloud-sdk/bin

RUN apt-get -qq update \
  && apt-get -qq --no-install-recommends -y install \
    procps \
    python

RUN mkdir -p /opt \
  && curl -sSL "${GCLOUD_SDK_URL}" | tar zx -C /opt \
  && /opt/google-cloud-sdk/install.sh -q \
  && gcloud config set disable_usage_reporting true \
  && gcloud components install app-engine-java