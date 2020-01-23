FROM ubuntu:16.04

ARG GIT_COMMIT=master
ARG GH_PR
ARG GH_SLUG=pocl/pocl
ARG LLVM_VERSION=6.0

LABEL maintainer="Matthieu Boileau <matthieu.boileau@math.unistra.fr>"
LABEL git-commit=$GIT_COMMIT vendor=pocl distro=Ubuntu version=1.0

USER root
ENV TERM dumb
RUN apt-get update && \
    apt-get -yq dist-upgrade && \
    apt-get install -y software-properties-common wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN add-apt-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-${LLVM_VERSION} main" && apt update
RUN apt-get update && \
    apt install -y build-essential \
                   cmake \
                   git \
                   pkg-config \
                   libclang-${LLVM_VERSION}-dev \
                   clang-${LLVM_VERSION} \
                   llvm-${LLVM_VERSION} \
                   make \
                   ninja-build \
                   ocl-icd-libopencl1 \
                   ocl-icd-dev \
                   ocl-icd-opencl-dev \
                   python3-pip \
                   libhwloc-dev \
                   zlib1g \
                   zlib1g-dev \
                   clinfo \
                   dialog \
                   apt-utils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN cd /home && \
    git clone https://github.com/$GH_SLUG.git && \
    cd /home/pocl && \
    git checkout $GIT_COMMIT && \
    test -z "$GH_PR" || (git fetch origin +refs/pull/$GH_PR/merge && git checkout -qf FETCH_HEAD) && \
    mkdir build && \
    cd build && \
    cmake -G Ninja -DWITH_LLVM_CONFIG=/usr/bin/llvm-config-${LLVM_VERSION} -DCMAKE_INSTALL_PREFIX=/usr .. && \
    ninja install && \
    cd .. && \
    rm -rf build

ADD requirements.txt /tmp
RUN pip3 install --no-cache-dir -r /tmp/requirements.txt

