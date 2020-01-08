ARG UBUNTU_RELEASE=xenial

FROM docker.io/sreejithpunnapuzha/ubuntu:${UBUNTU_RELEASE}
LABEL maintainer="sreejith.punnapuzha@outlook.com"

ARG version=3.6.0

RUN set -xe \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt update && apt dist-upgrade -y \
    && apt update && apt install -y python3 python3-pip libffi-dev libssl-dev \
    && pip3 install nodepool==$version \
    && rm -rf ~/.cache/pip \
    && apt remove --purge -y python3-pip libffi-dev libssl-dev \
    && apt autoremove -y && apt clean && rm -rf /var/lib/apt/lists/* \
    && adduser --system nodepool --home /var/lib/nodepool 

USER nodepool:nodepool
ENTRYPOINT ["nodepool-launcher", "-d", "-c", "/etc/nodepool/nodepool.yaml"]
