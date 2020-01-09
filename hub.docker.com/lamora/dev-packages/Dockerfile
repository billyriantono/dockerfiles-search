# ------------------------------------------------------------------------------
# Based on a work at https://github.com/docker/docker.
# ------------------------------------------------------------------------------
# Pull base image.
FROM ubuntu:bionic
MAINTAINER Lucius Amora <reture@msn.com>

# ------------------------------------------------------------------------------
# Install Packages
RUN apt update \
    && apt install -y curl supervisor nodejs git build-essential nginx \
    sshfs openssh-server net-tools vim man autoconf \
    libfuse-dev libboost-all-dev libssl-dev libxml2-dev \
    golang rustc cmake luajit python3 ruby default-jdk flex bison
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|apt-key add - \
    && echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic main" \
    > /etc/apt/sources.list.d/llvm.list
RUN apt update && apt install -y clang-tools-8 libclang-8-dev libllvm8 llvm-8-dev lldb-8 lld-8 \
    && sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
