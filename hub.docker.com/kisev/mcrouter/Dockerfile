FROM ubuntu:14.04

ARG MCROUTER_BRANCH=release-37-0
ARG MCROUTER_DIR=/usr/local/mcrouter

ENV MCROUTER_REPO=https://github.com/facebook/mcrouter.git
ENV DEBIAN_FRONTEND=noninteractive

# Install build requirements
RUN apt-get -qq update && \
    apt-get -qq -y install \
      sudo \
      git \
      software-properties-common && \
    add-apt-repository -y ppa:george-edison55/cmake-3.x && \
    apt-get -qq update && \
    apt-get -qq -y install cmake

# Build sources
RUN mkdir -p ${MCROUTER_DIR}/repo && \
    cd ${MCROUTER_DIR}/repo && \
    git clone ${MCROUTER_REPO} && \
    cd ${MCROUTER_DIR}/repo/mcrouter/mcrouter/scripts && \
    git checkout ${MCROUTER_BRANCH} && \
    ./install_ubuntu_14.04.sh ${MCROUTER_DIR} && \
    ./clean_ubuntu_14.04.sh ${MCROUTER_DIR} && \
    rm -rf ${MCROUTER_DIR}/repo && \
    ln -s ${MCROUTER_DIR}/install/bin/mcrouter /usr/local/bin/mcrouter

ENV DEBIAN_FRONTEND=newt
