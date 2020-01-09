FROM debian:stable
MAINTAINER Alex, Jiang <alexxyjiang@gmail.com>
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV DEPENDENCIES asciidoc autoconf automake build-essential git libc-ares-dev libev-dev libmbedtls-dev libpcre3-dev libsodium-dev libtool
ENV REMOTE_SRC https://github.com/shadowsocks/shadowsocks-libev.git
RUN apt update --fix-missing
RUN apt install -y $DEPENDENCIES
RUN cd ~ \
    && git clone ${REMOTE_SRC} \
    && cd ~/shadowsocks-libev/ \
    && git checkout `git tag | sort | tail -1` \
    && git submodule update --init --recursive
RUN cd ~/shadowsocks-libev && ./autogen.sh && ./configure && make && make install
ENTRYPOINT ["ss-server"]
