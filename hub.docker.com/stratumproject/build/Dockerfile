# Not supported with default docker version on Ubuntu 14.04 (1.13)
# ARG DEBIAN_TAG=jessie
# FROM debian:${DEBIAN_TAG}
FROM debian:jessie
LABEL maintainer="Stratum dev <stratum-dev@lists.stratumproject.org>"
LABEL description="This Docker image sets up a development environment for Stratum"

ARG BAZEL_VERSION=0.14.1

# bazel dependencies
# + wget to download bazel binary
# + ca-certificates for wget HTPPS connection
ENV PKG_DEPS pkg-config zip g++ zlib1g-dev unzip python wget ca-certificates \
    ssh git gdb vim emacs-nox sudo libudev-dev libjudy-dev bison flex \
    libfl-dev libgmp-dev libi2c-dev

RUN apt-get update && \
    apt-get install -y --no-install-recommends $PKG_DEPS

RUN wget https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VERSION/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    chmod +x bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    ./bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    rm -f bazel-$BAZEL_VERSION-installer-linux-x86_64.sh

