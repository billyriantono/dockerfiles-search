FROM alpine:3.8

LABEL maintainer "Daniel Vincenzi <danielvincenzi@icloud.com>"

ENV HELM_VERSION "v2.11.0"
ENV GCLOUD_SDK_VERSION "228.0.0"
ENV GCLOUD_SDK_URL "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-$GCLOUD_SDK_VERSION-linux-x86_64.tar.gz"
ENV PATH "$PATH:/opt/google-cloud-sdk/bin"

RUN \
    # Install dependencies 
    apk add --update --no-cache \
      ca-certificates \
      curl \
      bash \
      python \
      tar \
      openssl \ 
      wget && \
    # Install Helm
    curl --output /tmp/helm-$HELM_VERSION-linux-amd64.tar.gz -L https://storage.googleapis.com/kubernetes-helm/helm-$HELM_VERSION-linux-amd64.tar.gz && \
    cd /tmp && \
    tar xvzf /tmp/helm-$HELM_VERSION-linux-amd64.tar.gz && \
    cp linux-amd64/helm /usr/local/bin/helm && \
    # Install Google Cloud SDK
    mkdir -p /opt && \
    cd /opt && \
    wget -q -O - $GCLOUD_SDK_URL | tar zxf - && \
    bash /opt/google-cloud-sdk/install.sh && \
    gcloud components install alpha beta kubectl && \
    # Cleanup
    rm -rf /tmp/* && \
    apk --purge del \
      curl \
      tar \
      wget
