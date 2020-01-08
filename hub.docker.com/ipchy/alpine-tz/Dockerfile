FROM alpine:3.6
MAINTAINER ipchy <ipchy@live.it>

ENV TZ Asia/Shanghai
ENV MIRROR_LIST mirrors.ustc.edu.cn
RUN sed -i "s/dl-cdn.alpinelinux.org/$MIRROR_LIST/" /etc/apk/repositories && \
    apk upgrade --no-cache && \
    apk add --no-cache tzdata 
