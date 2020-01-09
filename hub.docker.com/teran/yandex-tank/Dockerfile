FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y \
        sudo \
        vim \
        wget \
        curl \
        less \
        iproute2 \
        software-properties-common \
        telnet \
        atop \
        openssh-client \
        git \
        python-pip \
        tmux && \
    add-apt-repository ppa:yandex-load/main -y && \
    apt-get update -q && \
    apt-get install -y --no-install-recommends --no-install-suggests \
        phantom \
        phantom-ssl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /tmp/* /var/tmp/*

RUN export BUILD_DEPS="python-dev build-essential gfortran libssl-dev libffi-dev" && \
    apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y ${BUILD_DEPS} && \
    pip install --upgrade setuptools && \
    pip install --upgrade pip==9.0.3 && \
    pip install https://api.github.com/repos/yandex/yandex-tank/tarball/master && \
    apt-get autoremove -y --purge ${BUILD_DEPS} && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /tmp/* /var/tmp/* /root/.cache/*
