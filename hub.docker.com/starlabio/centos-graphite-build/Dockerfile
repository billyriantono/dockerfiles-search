FROM starlabio/centos-base:3
MAINTAINER David Esler <adam.schwalm@starlab.io>

RUN yum install -y libidn-devel zlib-devel ncurses-devel dev86 iasl \
        gettext openssl-devel pciutils-devel libuuid-devel \
        bzip2-devel xz-devel e2fsprogs e2fsprogs-devel yajl-devel mingw64-binutils \
        systemd-devel glibc-devel.i686 texinfo && \
        yum clean all && \
        rm -rf /var/cache/yum/* /tmp/* /var/tmp/*
