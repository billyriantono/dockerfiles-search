FROM alpine:3.8
ENV CLOUD_SDK_VERSION=190.0.1
ENV PATH=/google-cloud-sdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apk update && \
  apk upgrade && \
  apk --no-cache add bash curl python py-crcmod libc6-compat openssh-client git


RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
  tar xzf google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
  rm google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
  ln -s /lib /lib64 && \
  gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud config set metrics/environment github_docker_image && \
  gcloud --version

VOLUME [/root/.config]

RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" > /etc/apk/repositories && \
  apk update && \
  apk add "postgresql@edge>10" "postgresql-client@edge>10" "postgresql-dev@edge>10" --no-cache

RUN apk add "redis@edge" --no-cache

RUN apk add --no-cache "mysql@edge" "mysql-client@edge"
