ARG ATOMIC_PARSLEY_VERSION=0.9.6
ARG ALPINE_VERSION=3.9
ARG ARCH=x86_64

FROM alpine:$ALPINE_VERSION as atomicparsley
ARG ARCH
RUN set -xe && \
    apk add --no-cache build-base \
      abuild \
      autoconf \
      automake \
      git \
      libtool \
      linux-headers \
      zlib-dev && \
    addgroup root abuild && \
    abuild-keygen -a && \
    mkdir /build && \
    git clone --depth 1 https://git.alpinelinux.org/aports /build

WORKDIR /build/testing/atomicparsley
RUN abuild -F checksum && \
    abuild -F -r && \
    ls -al ~/packages/testing/$ARCH



FROM wernight/youtube-dl
ARG ARCH
ARG ATOMIC_PARSLEY_VERSION
COPY --from=atomicparsley /root/packages/testing/${ARCH}/atomicparsley-${ATOMIC_PARSLEY_VERSION}-r1.apk .
RUN set -xe && \
    apk add --no-cache --allow-untrusted ./atomicparsley-${ATOMIC_PARSLEY_VERSION}-r1.apk

