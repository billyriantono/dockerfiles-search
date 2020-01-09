FROM debian:jessie

LABEL maintainer "opsxcq@strm.sh"

RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ca-certificates \
    bc \
    u-boot-tools \
    binutils-arm-linux-gnueabihf \
    build-essential \
    ccache \
    gcc-arm-linux-gnueabihf \
    gccgo-4.7-arm-linux-gnueabi \
    git \
    libncurses-dev \
    libssl-dev \
    u-boot-tools \
    curl \
    wget \
    xz-utils \
    build-dep linux-image-$(uname -r) && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

VOLUME /data
WORKDIR /data

COPY main.sh /

ENTRYPOINT ["/main.sh"]
CMD ["default"]

