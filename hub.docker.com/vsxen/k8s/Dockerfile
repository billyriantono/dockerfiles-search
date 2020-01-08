FROM alpine:3.6
RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
     apk add --no-cache tcpdump netcat-openbsd socat curl bind-tools && \
     rm -rf /var/cache/apk/*
RUN ["/bin/sh"]