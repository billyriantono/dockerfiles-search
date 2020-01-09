# vim:set ft=dockerfile:
FROM alpine:3.4

MAINTAINER deinspanjer@gmail.com

RUN apk update && \
    apk upgrade && \
    apk add --update \
        bash \
        ca-certificates \
        coreutils \
        curl \
        gawk \
        gzip \
        sed \
        tar \
        wget \
        xz

RUN wget --no-check-certificate https://raw.github.com/tokland/arch-bootstrap/master/arch-bootstrap.sh

RUN mkdir arch_chroot

RUN bash arch-bootstrap.sh -a x86_64 -r http://mirror.rackspace.com/archlinux/ arch_chroot

COPY start_chroot.sh /

COPY setup_base_arch_env.sh /arch_chroot
COPY setup_postgrest_arch_env.sh /arch_chroot

RUN chmod u+x start_chroot.sh /arch_chroot/*.sh
