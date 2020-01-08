# Make NKF
FROM frolvlad/alpine-glibc AS build-nkf

WORKDIR /nkf
ENV NKF_VERSION 2.1.5
RUN apk update && \
    apk add \
      curl musl-dev gcc make g++ file alpine-sdk && \
    curl -vLO https://ja.osdn.net/dl/nkf/nkf-${NKF_VERSION}.tar.gz && \
    tar zxvf nkf-${NKF_VERSION}.tar.gz && \
    cd nkf-${NKF_VERSION} && \
    make && \
    make install

# Build with cURL and NKF
FROM odise/busybox-curl
COPY --from=build-nkf /usr/local/bin/nkf /usr/local/bin/nkf
COPY --from=build-nkf /lib/ld-musl-x86_64.so.1 /lib/ld-musl-x86_64.so.1
RUN ln -s /lib/ld-musl-x86_64.so.1 /lib/libc.musl-x86_64.so.1
