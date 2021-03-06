FROM debian:buster AS builder

# Download QEMU, see https://github.com/docker/hub-feedback/issues/1261
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    apt-utils \
  && rm -rf /var/lib/apt/lists/* \
  && apt -qyy clean
RUN export QEMU_USER_STATIC_LATEST_TAG=$(curl -s https://api.github.com/repos/multiarch/qemu-user-static/tags \
        | grep 'name.*v[0-9]' | head -n 1 | cut -d '"' -f 4) && \
    curl -SL "https://github.com/multiarch/qemu-user-static/releases/download/${QEMU_USER_STATIC_LATEST_TAG}/x86_64_qemu-arm-static.tar.gz" \
        | tar xzv --directory /

FROM arm32v7/debian

COPY --from=builder /qemu-arm-static /usr/bin/

MAINTAINER Guy Sheffer <guysoft at gmail dot com>

RUN set -x \
    && apt-get update && apt-get install -y \
        build-essential \
        curl \
        git \
        wget \
        p7zip-full \
        python3 \
        binfmt-support \
        qemu \
        sudo \
        zip \
        lsof \
    && rm -rf /var/lib/apt/lists/*

COPY . /CustomPiOS

CMD ["/bin/bash"]
