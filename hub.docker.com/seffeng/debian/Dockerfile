FROM debian:buster-slim

MAINTAINER  seffeng "seffeng@sina.cn"

RUN \
 sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list &&\
 sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list &&\
 apt-get clean &&\
 rm -rf /var/cache/apk/*

CMD ["bash"]