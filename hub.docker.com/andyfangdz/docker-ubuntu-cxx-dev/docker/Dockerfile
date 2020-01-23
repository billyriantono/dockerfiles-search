FROM ubuntu:18.04 AS ghdl-builder
LABEL maintainer="andrsmllr <andrsmllr@bananatronics.org>"
LABEL description="GHDL open source VHDL simulator"
LABEL version="1.0"
ARG GHDL_VERSION=v0.36
ARG GHDL_BACKEND=mcode

ENV TERM=xterm-256color
VOLUME /workdir
WORKDIR /workdir
# GHDL build parameters.
ENV GHDL_BACKEND=${GHDL_BACKEND}
ENV GHDL_VERSION=${GHDL_VERSION}
ENV GHDL_PATH=/opt/ghdl-${GHDL_BACKEND}-${GHDL_VERSION}
ENV GHDL_SRC=/usr/src/ghdl
# Supported backend version may depend on GHDL version.
ENV LLVM_VERSION=7
#RUN export GCC_VERSION=$(gcc --version | sed -n 1p | rev | cut -d" " -f1 | rev)
#RUN export GCC_MAJOR_VERSION=$(echo $GCC_VERSION | head -c 1)
ENV GCC_VERSION=7.4
ENV GCC_MAJOR_VERSION=7

# Get GHDL sources and common dependencies.
RUN apt update -qq \
    && apt install --no-install-recommends -qq -y \
        git \
        gnat \
        make \
        libz-dev \
        ca-certificates \
    && apt autoclean && apt clean && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/ghdl/ghdl $GHDL_SRC \
    && cd ${GHDL_SRC} \
    && git checkout ${GHDL_VERSION}
# Build with mcode backend. This takes no time to build.
RUN if [ ${GHDL_BACKEND} = mcode ]; then \
    cd ${GHDL_SRC} \
    && ./configure \
        --prefix=${GHDL_PATH} \
    && make && make install \
    && ln -s ${GHDL_PATH} /opt/ghdl \
    && ln -s /opt/ghdl/bin/ghdl /usr/bin/ghdl \
    ; fi
# Build with llvm backend. This takes some time to build.
RUN if [ ${GHDL_BACKEND} = llvm ]; then \
    apt update -qq \
    && apt install --no-install-recommends -qq -y \
        llvm-${LLVM_VERSION} \
        llvm-${LLVM_VERSION}-dev \
        clang++-${LLVM_VERSION} \
        libedit-dev gcc-${GCC_MAJOR_VERSION} \
    && apt autoclean && apt clean && rm -rf /var/lib/apt/lists/* \
    && ln -s /usr/bin/clang++-${LLVM_VERSION} /usr/bin/clang++ \
    && cd ${GHDL_SRC} \
    && ./configure \
        --prefix=${GHDL_PATH} \
        --with-llvm-config=/usr/bin/llvm-config-${LLVM_VERSION} \
    && make && make install \
    && ln -s ${GHDL_PATH} /opt/ghdl \
    && ln -s /opt/ghdl/bin/ghdl /usr/bin/ghdl \
    ; fi
# Build with gcc backend. This takes a very long time to build. Does not work yet.
RUN if [ ${GHDL_BACKEND} = gcc ]; then \
    apt update -qq \
    && apt install --no-install-recommends -qq -y \
        gcc-${GCC_MAJOR_VERSION} \
        g++-${GCC_MAJOR_VERSION} \
        gnat-${GCC_MAJOR_VERSION} \
        gcc-${GCC_MAJOR_VERSION}-source \
        xz-utils \
    && apt clean \
    && cd /usr/src/gcc-${GCC_MAJOR_VERSION} \
    && tar xf $(find . -maxdepth 1 -type f -name "gcc-${GCC_VERSION}*") \
    && cd $(find . -maxdepth 1 -type d -name "gcc-${GCC_VERSION}*") \
    && ./contrib/download_prerequisites \
    && cd ${GHDL_SRC} \
    && ./configure \
      --prefix=${GHDL_PATH}-gcc \
      --with-gcc=/usr/src/gcc-${GCC_MAJOR_VERSION}/gcc-${GCC_VERSION}.0 \
    && make copy-sources \
    && cd /usr/src/gcc-${GCC_MAJOR_VERSION}/gcc-${GCC_VERSION}.0 \
    && ./configure \
      --prefix=${GHDL_PATH}-gcc \
      --disable-multilib \
    && make && make install \
    && cd ${GHDL_SRC} \
    && make && make install \
    && ln -s ${GHDL_PATH}-gcc/bin/ghdl /usr/bin/ghdl \
    ; fi
ENTRYPOINT ["/usr/bin/ghdl"]
CMD ["--help"]

# TODO: pre-compile libraries.
#ENV XILINX_UNISIM_SRC
#ENV XILINX_UNIMACRO_SRC
#ENV XILINX_XILINXCORELIB_SRC
#ENV OSVVM_SRC
#ENV VUNIT_SRC
