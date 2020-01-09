FROM amazonlinux:2018.03

MAINTAINER Bitnami <containers@bitnami.com>

RUN yum update -y && yum install -y git diffutils gcc gcc-c++ make openssl-devel glibc-devel cmake clang ncurses-devel automake m4 gperf zip file rsync libtool unzip which

ENV NAMI_VERSION=1.0.0-1

RUN cd /tmp && \
    curl -sSLO https://nami-prod.s3.amazonaws.com/tools/nami/releases/nami-$NAMI_VERSION-linux-x64.tar.gz && \
    echo "80488279b056d5e9c183fe34097c5f496715ab16a602afcc9f78d59f15139a16  nami-$NAMI_VERSION-linux-x64.tar.gz" | sha256sum -c - && \
    mkdir -p /opt/bitnami/nami && \
    tar xzf nami-$NAMI_VERSION-linux-x64.tar.gz --strip 1 -C /opt/bitnami/nami && \
    rm nami-$NAMI_VERSION-linux-x64.tar.gz

ENV PATH=/opt/bitnami/nami/bin:$PATH

COPY rootfs /
