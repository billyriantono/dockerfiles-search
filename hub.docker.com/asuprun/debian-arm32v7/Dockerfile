FROM debian:stretch AS build

ENV RESIN_XBUILD_URL https://github.com/aleksey-suprun/resin-xbuild/releases/download/v0.1.0/resin-xbuild-0.1.0.tar.gz
ENV QEMU_URL https://github.com/resin-io/qemu/releases/download/v2.9.0%2Bresin1/qemu-2.9.0.resin1-arm.tar.gz

ADD $QEMU_URL /root/qemu.tar.gz
ADD $RESIN_XBUILD_URL /root/resin-xbuild.tar.gz

RUN mkdir /root/bin
RUN tar --strip-components=1 -C /root/bin -xzf /root/resin-xbuild.tar.gz
RUN tar --strip-components=1 -C /root/bin -xzf /root/qemu.tar.gz

FROM arm32v7/debian:stretch

COPY --from=build /root/bin/ /usr/bin/
