# Pull base image.
FROM ubuntu:14.04

MAINTAINER Tyson Thomas, tysonthomas.90@gmail.com

#Set sh as bash 
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget python-pip nano supervisor && \
  rm -rf /var/lib/apt/lists/*

RUN echo "deb http://www.openfoam.org/download/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/openfoam.list
RUN echo "2014-10-02.1";apt-get update 

### Openfoam
RUN apt-get install -y \
    libgl1-mesa-glx libgmp10 libqt4-opengl libqtcore4 libqtgui4 \
    binutils cpp-4.4 g++-4.4 gcc-4.4 gcc-4.4-base libstdc++6-4.4-dev \
    libibverbs-dev libopenmpi-dev openmpi-common  mpi-default-dev \
    libc-bin libc-dev-bin libc6 libc6-dev libdrm-dev libdrm-nouveau2 libgl1-mesa-dev libglu1-mesa libglu1-mesa-dev \
    libgmp-dev libgmpxx4ldbl libicu52 libmpfr-dev libmpfr4 libnuma1 libpthread-stubs0-dev \
    libqt4-designer libqt4-dev libqt4-help libqt4-opengl-dev libqt4-qt3support libqt4-scripttools libqt4-svg libqt4-test \
    libqtwebkit-dev libqtwebkit4 libtorque2 \
    libx11-dev libx11-doc libxau-dev libxcb1-dev libxdmcp-dev libxext-dev linux-libc-dev manpages manpages-dev \
    mesa-common-dev qt4-linguist-tools qt4-qmake \
    x11proto-core-dev x11proto-input-dev x11proto-kb-dev x11proto-xext-dev xorg-sgml-doctools xtrans-dev zlib1g-dev \
    libscotch-5.1 libscotch-dev \
    binutils

RUN apt-get install -y --force-yes openfoam231

# Set OpenFoam ENV
RUN echo "source /opt/openfoam231/etc/bashrc" >> /root/.bashrc
RUN source /opt/openfoam231/etc/bashrc

# Install Node
# gpg keys listed at https://github.com/nodejs/node
RUN set -ex \
  && for key in \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
  ; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done

ENV NODE_VERSION 0.12.13
ENV NPM_VERSION 2.15.0

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
	&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
	&& gpg --verify SHASUMS256.txt.asc \
	&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
	&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
	&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc \
	&& npm install -g npm@"$NPM_VERSION" \
	&& npm cache clear

#Application dependency
RUN npm install -g grunt-cli

#Install AWS CLI
RUN pip install awscli