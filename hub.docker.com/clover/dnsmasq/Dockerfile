FROM library/ubuntu:bionic AS build

ENV LANG=C.UTF-8
RUN export DEBIAN_FRONTEND=noninteractive \
 && apt-get update \
 && apt-get install -y \
        software-properties-common \
        apt-utils

RUN mkdir -p /build /rootfs
WORKDIR /build
RUN apt-get download \
        dnsmasq \
        dnsmasq-base-lua \
        libgmp10 \
        libhogweed4 \
        libidn11 \
        libnetfilter-conntrack3 \
        libnettle6 \
        libdbus-1-3 \
        liblua5.2-0 \
        libmnl0 \
        libnfnetlink0 \
        libsystemd0 \
        libgcrypt20 \
        liblz4-1 \
        liblzma5 \
        libstdc++6 \
        libgpg-error0

RUN find *.deb | xargs -I % dpkg-deb -x % /rootfs

WORKDIR /rootfs
RUN rm -rf \
        etc/* \
        lib/systemd \
        usr/lib/resolvconf \
        usr/share \
        var \
    echo > /etc/dnsmasq.conf

COPY init/ etc/init/

WORKDIR /


FROM clover/base

ENV LANG=C.UTF-8

COPY --from=build /rootfs /

EXPOSE 53
