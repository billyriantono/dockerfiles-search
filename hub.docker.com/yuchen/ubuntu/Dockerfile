FROM ubuntu:16.04

ADD sources.list /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
    tzdata \
    tree \
    file \
    stress \
    stress-ng \
    iputils-ping \
    iproute2 \
    netcat-openbsd \
    net-tools \
    dnsutils \
    curl \
    socat \
    iptables \
    arping \
    ethtool \
    bc \
    && rm -rf /var/lib/apt/lists/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata
