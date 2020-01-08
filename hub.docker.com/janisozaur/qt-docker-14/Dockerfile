FROM ubuntu:14.04
ENV XXDEBIAN_FRONTEND noninteractive
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    apt-add-repository -y ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get install -y gcc-6 g++-6 gcc-5 g++-5 && \
    apt-get -qq clean
RUN apt-get -qq update && apt-get -qq dist-upgrade && apt-get install -qq -y --no-install-recommends \
    git \
    openssh-client \
    ca-certificates \
    make \
    default-jdk \
    ant \
    curl \
    p7zip \
    libsm6 \
    libice6 \
    libxext6 \
    libxrender1 \
    libfontconfig1 \
    libxcb-xinerama0-dev \
    && apt-get -qq clean
RUN apt-get -qq -y build-dep libqt5core5a libqt5qml5 libqt5quick5 && apt-get -qq clean
