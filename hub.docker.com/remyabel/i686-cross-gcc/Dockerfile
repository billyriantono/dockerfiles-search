FROM alpine:edge AS build

ENV GCC_MIRROR https://ftpmirror.gnu.org/

ENV GCC_VERSION 9.1.0
ENV BINUTILS_VERSION 2.31

WORKDIR /tmp/

RUN apk update && apk add build-base curl libc6-compat

RUN curl -fL "$GCC_MIRROR/binutils/binutils-$BINUTILS_VERSION.tar.xz" -o "binutils.tar.xz"
RUN curl -fL "$GCC_MIRROR/gcc/gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz" -o "gcc.tar.xz"
RUN mkdir -p binutils && mkdir -p gcc
RUN tar -xf binutils.tar.xz -C ./binutils --strip-components=1
RUN tar -xf gcc.tar.xz -C ./gcc --strip-components=1
RUN mkdir -p build-binutils && cd build-binutils && \
        ../binutils/configure --prefix=/tmp/install --target=i686-elf --with-sysroot --disable-nls --disable-werror
RUN cd build-binutils && \
        make -j4 && \
        make install
RUN cd /tmp/gcc && ./contrib/download_prerequisites
RUN cd /tmp/ && mkdir -p build-gcc && cd build-gcc && \
        ../gcc/configure --prefix=/tmp/install --target=i686-elf --disable-nls --enable-languages=c,c++ --without-headers
RUN cd build-gcc && \
        make -j4 all-gcc && \
        make -j4 all-target-libgcc && \
        make install-gcc && \
        make install-target-libgcc

FROM alpine:edge

RUN apk update \
    && apk add nasm cmake make libc6-compat

COPY --from=build /tmp/install/ $HOME/cross-install
ENV PATH=$HOME/cross-install/bin:$PATH
ENV LD_LIBRARY_PATH=$HOME/cross-install/lib:$HOME/cross-install/lib64:$PATH
