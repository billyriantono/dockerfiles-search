ARG UBUNTU_RELEASE=xenial

FROM docker.io/sreejithpunnapuzha/ubuntu:${UBUNTU_RELEASE}
LABEL maintainer="sreejith.punnapuzha@outlook.com"

WORKDIR /usr/src/nodepool-config-builder

COPY requirements.txt .

RUN set -xe \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt update && apt dist-upgrade -y \
    && apt install -y python3 python3-pip build-essential openssl libffi-dev libssl-dev make gcc musl-dev python3-dev \
    && pip3 install -r requirements.txt \
    && rm -rf ~/.cache/pip \
    && apt remove --purge -y python3-pip build-essential openssl libffi-dev libssl-dev make gcc musl-dev python3-dev \
    && apt autoremove -y && apt clean && rm -rf /var/lib/apt/lists/* 

COPY . .

ENTRYPOINT ["/usr/src/nodepool-config-builder/nodepool-config-builder.py"]
