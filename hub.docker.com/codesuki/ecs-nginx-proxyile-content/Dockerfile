# Build image
FROM codereaper91/gcc:8.3.0 as build

## Build environment
ENV PREFIX=/opt/cross
ENV TARGET=arm-none-eabi
ENV PATH="${PREFIX}/bin:${PATH}"
WORKDIR /usr/src

## Install dependencies
RUN apk add --no-cache bison flex gmp-dev mpc1-dev mpfr-dev

## Download source code
RUN mkdir -p binutils gcc && \
    wget -qO- https://ftp.gnu.org/gnu/binutils/binutils-2.32.tar.gz  | tar -xz && \
    wget -qO- https://ftp.gnu.org/gnu/gcc/gcc-8.3.0/gcc-8.3.0.tar.gz | tar -xz

## Build binutils
WORKDIR /usr/src/build-binutils
RUN ../binutils-2.32/configure --target=$TARGET --prefix="$PREFIX" --with-sysroot --disable-nls --disable-werror && \
    make && make install

## Build gcc
WORKDIR /usr/src/build-gcc
RUN ../gcc-8.3.0/configure --target=$TARGET --prefix="$PREFIX" --disable-nls --enable-languages=c,c++ --without-headers && \
    make all-gcc && make all-target-libgcc && \
    make install-gcc && make install-target-libgcc

# Base image
FROM codereaper91/gcc:8.3.0

## Environment
ENV CROSS_COMPILER="/opt/cross"
ENV TARGET=arm-none-eabi
ENV PATH="${CROSS_COMPILER}/bin:${PATH}"

## Files
COPY --from=build /opt/cross /opt/cross

## Entry point command
CMD [ "make" ]