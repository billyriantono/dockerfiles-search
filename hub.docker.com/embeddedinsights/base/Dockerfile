FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
	git \
        make \
        ninja-build \
        python3 \
        python3-pip \
        wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install setuptools \
    && pip3 install wheel \
    && pip3 install meson

