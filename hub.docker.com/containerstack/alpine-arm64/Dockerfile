FROM scratch
LABEL maintainer="Remon Lam [remon@containerstack.io]" architecture="ARM64/aarch64"

ENV ALPINE_ARCH aarch64
ENV ALPINE_VERSION 3.7.0

ADD alpine-minirootfs-${ALPINE_VERSION}-${ALPINE_ARCH}.tar.gz /
CMD ["/bin/sh"]
