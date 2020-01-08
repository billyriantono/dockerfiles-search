FROM debian:stretch

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        libgmp-dev libmpfr-dev libmpc-dev \
        wget ca-certificates \
    && rm -rf /var/lib/apt/lists/*

ENV GCC_VERSION 7.4.0

RUN set -xe \
    && wget ftp://ftp.gnu.org/gnu/gcc/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.gz \
    && tar xf gcc-${GCC_VERSION}.tar.gz

RUN set -xe \
    cd gcc-${GCC_VERSION} \
    && mkdir build \
    && cd build \
    && ../gcc-${GCC_VERSION}/configure -v \
        --build=x86_64-linux-gnu \
        --host=x86_64-linux-gnu \
        --target=x86_64-linux-gnu \
        --enable-checking=release \
        --enable-languages=c,c++,fortran \
        --disable-multilib \
        --program-suffix=-${GCC_VERSION} \
    && make -j"$(grep -c ^processor /proc/cpuinfo)" \
    && make install \
    && cd .. \
    && rm -rf gcc-$GCC_VERSION \
    && rm -rf build

RUN update-alternatives \
        --install /usr/bin/gcc gcc /usr/local/bin/gcc-${GCC_VERSION} 100 \
        --slave /usr/bin/g++ g++ /usr/local/bin/g++-${GCC_VERSION}