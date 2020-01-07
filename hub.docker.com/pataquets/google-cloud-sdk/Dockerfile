FROM pataquets/ubuntu:xenial

# Based on https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu
RUN \
  . /etc/lsb-release && \
  echo "deb http://packages.cloud.google.com/apt cloud-sdk-${DISTRIB_CODENAME} main" | \
    tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
  apt-key adv --keyserver hkp://hkps.pool.sks-keyservers.net --recv-keys 3746C208A7317B0F \
  && \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get install -y google-cloud-sdk \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
