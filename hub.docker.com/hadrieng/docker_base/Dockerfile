FROM debian:jessie

MAINTAINER Hadrien Gourlé <gourlehadrien@gmail.com>

RUN apt-get update --fix-missing && apt-get install -y \
    wget \
    gcc \
    g++ \
    git \
    unzip \
    make \
    curl \
    python \
    lbzip2 zlib1g-dev libncurses5-dev \
    bzip2 && \
    apt-get clean

# Create the home folder
RUN mkdir -p /root
ENV HOME /root
