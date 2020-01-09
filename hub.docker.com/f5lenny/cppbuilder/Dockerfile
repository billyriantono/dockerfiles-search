FROM        ubuntu:wily
MAINTAINER  Lenny Maiorani <ldm5180@gmail.com>

# Default command on startup.
CMD bash

# Setup packages.
RUN apt-get update
RUN apt-get -y install \
    clang \
    clang-format-3.6 \
    cmake \
    debian-archive-keyring \
    debootstrap \
    devscripts \
    dh-make \
    git \
    libgtest-dev \
    pbuilder \
    pbuilder-scripts pv
RUN ln -s `which clang-format-3.6` /usr/local/bin/clang-format
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
RUN apt-get install git-lfs
RUN update-alternatives --set cc /usr/bin/clang
RUN update-alternatives --set c++ /usr/bin/clang++
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
