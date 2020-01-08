FROM nvidia/cuda:9.1-cudnn7-devel

## Cmake
RUN apt-get update -y --allow-unauthenticated && apt-get upgrade -y --allow-unauthenticated \
    && apt-get install curl wget unzip -y --allow-unauthenticated \
    && curl https://cmake.org/files/v3.11/cmake-3.11.4-Linux-x86_64.sh -o /tmp/curl-install.sh \
    && chmod u+x /tmp/curl-install.sh \
    && mkdir /usr/bin/cmake \
    && /tmp/curl-install.sh --skip-license --prefix=/usr/bin/cmake \
    && rm /tmp/curl-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"
