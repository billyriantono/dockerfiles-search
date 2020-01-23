# Alpine with apk using Chinese mirror
FROM alpine:latest

LABEL maintainer="m@abreto.net"

RUN sed -i s/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g /etc/apk/repositories

CMD ["/bin/sh"]
