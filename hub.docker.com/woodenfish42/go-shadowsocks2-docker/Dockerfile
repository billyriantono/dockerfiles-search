#
# Dockerfile for go-shadowsocks2
#

FROM busybox:uclibc AS download-env

ENV SS_VER v0.0.11
ENV SS_URL https://github.com/shadowsocks/go-shadowsocks2/releases/download/$SS_VER/shadowsocks2-linux.gz

ADD $SS_URL /
RUN gunzip shadowsocks2-linux.gz && chmod +x shadowsocks2-linux

FROM scratch
COPY --from=download-env /shadowsocks2-linux /shadowsocks2-linux

ENTRYPOINT ["/shadowsocks2-linux"]
