FROM debian:stretch-slim

ARG DEBIAN_FRONTEND=noninteractive

# Docker for Jenkins really needs procps otherwise the Jenkins side fails
RUN apt-get update && apt-get install --no-install-recommends -y procps

# Set HOME to a writable directory in case something wants to cache things
# (e.g. obs)
ENV HOME=/tmp
ENV GOPATH=/usr/local/go
ENV PATH=$PATH:/usr/local/go/bin

# SSL / HTTPS support
RUN apt-get update && apt-get install --no-install-recommends -y \
    apt-transport-https \
    ca-certificates

# Dependencies to build debos
RUN apt-get update && apt-get install --no-install-recommends -y \
    golang-go \
    git \
    libostree-dev \
    gcc \
    libc6-dev

# Build debos
RUN go get github.com/go-debos/debos/cmd/debos && \
    go install github.com/go-debos/debos/cmd/debos

# Dependencies to run debos
RUN apt-get update && apt-get install --no-install-recommends -y \
    debootstrap \
    pkg-config \
    busybox \
    linux-image-amd64 \
    qemu-system-x86 \
    qemu-user-static \
    systemd-container \
    binfmt-support \
    parted \
    dosfstools \
    e2fsprogs

# Extra packages needed by kernelCI
RUN apt-get update && apt-get install --no-install-recommends -y \
    python \
    python-requests \
    xz-utils

