FROM ubuntu:16.04

ARG PROJECT_DIR="/home/build/project"

## Install dependencies to build yocto linux image and electron
RUN apt-get update -qq \
    && apt-get install -y -qq \
    git \
    wget \
    curl \
    build-essential \
    libncurses5-dev \
    gcc \
    lib32stdc++6  \
    lib32z1 \
    libc6-i386 \
    lib32stdc++6 \
#    zlib1g:i386 \
    zlib1g \
    lzop \
    u-boot-tools \
    lzop \
    gawk \
    wget \
    git-core \
    diffstat \
    unzip \
    texinfo \
    gcc-multilib \
    chrpath \
    socat \
    libsdl1.2-dev \
    xterm \
    clang \
    libdbus-1-dev \
    libgtk2.0-dev \
    libnotify-dev \
    libgnome-keyring-dev \
    libgconf2-dev \
    libasound2-dev \
    libcap-dev \
    libcups2-dev \
    libxtst-dev \
    libxss1 \
    libnss3-dev \
    g++-multilib \
    gperf \
    bison

RUN apt-get update -qq && \
    apt-get install -y -qq \
    fakeroot \
    ncurses-dev \
    xz-utils \
    libssl-dev \
    bc

RUN apt-get update -qq && \
    apt-get install -y -qq \
    cpio

# For development machine apt cache clean is not necessary
# RUN apt-get clean \
#	&& rm -rf /var/lib/apt/lists/* \
#	/tmp/* \
#	/var/tmp/*

# Create a non-root user that will perform the actual build
RUN id build 2>/dev/null || useradd --uid 30000 --create-home build
RUN echo "build ALL=(ALL) NOPASSWD: ALL" | tee -a /etc/sudoers

USER build

RUN mkdir -p $PROJECT_DIR
WORKDIR $PROJECT_DIR

