FROM ubuntu:18.04
LABEL maintainer="Corelight AWS Team <aws@corelight.com>"
LABEL description="Ubuntu with tooling for building C, signing packages"

RUN apt-get update && apt install -y \
    automake \
    autoconf \
    cmake \
    curl \
    jq \
    libssl1.0-dev \
    libtool \
    opensc \
    openssl \
    pkg-config \
 && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/bin/bash", "-l", "-c"]
