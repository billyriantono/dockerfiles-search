FROM alpine:latest
MAINTAINER  wj
RUN apk add --no-cache tzdata ca-certificates \
    &&ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asi a/Shanghai" > /etc/timezone \

## 注意：ca-certificates必须要有，否则https访问会失败