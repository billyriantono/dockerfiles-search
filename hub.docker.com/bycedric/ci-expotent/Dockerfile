# The offical swift docker is not used due to a compatibility issue with npm
# npm is required to install kitura on ubuntu
FROM ubuntu:18.04
LABEL maintainer="Bryan Flood <bryanfloodcontact@gmail.com>"
LABEL description="🐳 Simple Dev Environment for Serverside Swift using 🕊️Kitura"
LABEL url="https://github.com/KnowledgePending/Kitura-Docker"
RUN apt-get -qq update  && \
    apt-get -qq upgrade && \
    apt-get -qq install clang \
    libicu-dev \
    build-essential \
    git \
    libpython-dev \
    libblocksruntime-dev \
    wget \
    libcurl3 \
    software-properties-common && \
    add-apt-repository ppa:ubuntu-toolchain-r/test && \
    apt-get -qq upgrade libstdc++6 && \
    wget https://swift.org/builds/swift-5.0.2-release/ubuntu1804/swift-5.0.2-RELEASE/swift-5.0.2-RELEASE-ubuntu18.04.tar.gz && \
    tar xvzf swift-5.0.2-RELEASE-ubuntu18.04.tar.gz   && \
    rm swift-5.0.2-RELEASE-ubuntu18.04.tar.gz        && \
    apt-get -qq install nodejs     \
    npm && \
    npm install -g kitura-cli
ENV PATH="/swift-5.0.2-RELEASE-ubuntu18.04/usr/bin:${PATH}"
RUN apt-get install -qq libcurl4-openssl-dev \
                        openssl \
                        libssl-dev
