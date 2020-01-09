FROM ubuntu:16.04
MAINTAINER alex

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y install software-properties-common \
    && add-apt-repository ppa:jonathonf/gcc-7.1 \
    && apt-get update \
    && apt-get -y install \
	    gcc-7 g++-7 \
            git build-essential cmake \
            libmicrohttpd10 libuv1 \
            libuv1-dev libmicrohttpd-dev \

        # Не тащим лишнего
        --no-install-recommends \

    # Install Xmrig 
    && mkdir -p /app && cd /app \
    && git clone https://github.com/xmrig/xmrig.git \
    && cd xmrig && mkdir build && cd build \
    && cmake .. -DCMAKE_C_COMPILER=gcc-7 -DCMAKE_CXX_COMPILER=g++-7 \
    && make \
    #&& make install \

    # Cleanup to keep the images size small
    && apt-get purge -y \
        gcc-7 g++-7 \
        build-essential cmake \
        libuv1-dev libmicrohttpd-dev \
    && apt-get autoremove -y \
    && rm -r /var/lib/apt/lists/*

WORKDIR /app/xmrig/build
ENV PATH /app/xmrig/build:$PATH
CMD ["/bin/sh", "-c","xmrig", "--help"]
