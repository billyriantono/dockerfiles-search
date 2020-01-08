FROM ubuntu:18.04
MAINTAINER Oscar Hellström <oscar.hellstrom@vinnter.se>
LABEL Description="Image for building mbed projects with the GNU Arm Embedded toolchain"

RUN apt-get update && apt-get install -y \
    software-properties-common \
    && add-apt-repository ppa:team-gcc-arm-embedded/ppa \
    && apt-get update \
    && apt-get install -y \
    libnss-wrapper \
    build-essential \
    cmake \
    gcc-arm-embedded \
    python3 \
    python3-pip \
    git \
    mercurial \
    zsh \
    bash-completion \
    locales \
    && apt-get purge software-properties-common -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN pip3 install mbed-cli && mbed toolchain -G GCC_ARM && rm -rf ~/.cache/pip/*

ADD run.sh /usr/local/bin/run.sh
ENTRYPOINT ["/usr/local/bin/run.sh"]
