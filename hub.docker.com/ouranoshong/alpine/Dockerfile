FROM alpine:edge

ENV LC_ALL zh_CN.UTF-8
ENV LC_LANG zn_CN.UTF-8

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apk/repositories

RUN apk --no-cache add tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" | tee /etc/timezone && \
    apk del tzdata

RUN apk --no-cache add bash
