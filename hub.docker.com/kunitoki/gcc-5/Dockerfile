FROM gcc:5
MAINTAINER Lucio Asnaghi <kunitoki@gmail.com>

RUN apt-get -qq update \
    && apt-get -qq install -y --no-install-recommends \
        ca-certificates \
        python \
        ninja-build \
        ccache \
        git \
    && apt-get clean \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

RUN curl -SL https://github.com/Kitware/CMake/releases/download/v3.14.6/cmake-3.14.6-Linux-x86_64.sh -o /tmp/curl-install.sh \
    && chmod u+x /tmp/curl-install.sh \
    && mkdir /usr/bin/cmake \
    && /tmp/curl-install.sh --skip-license --prefix=/usr/bin/cmake \
    && rm /tmp/curl-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"
