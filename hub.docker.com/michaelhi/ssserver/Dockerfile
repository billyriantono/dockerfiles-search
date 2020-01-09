FROM alpine:latest
MAINTAINER michaelhe<mching.08@gmail.com>

RUN apk update  && \
    apk add py-pip && \
    pip install --upgrade pip && \
    pip install shadowsocks

# 对外暴露8388端口
EXPOSE 8388

RUN adduser -D app
USER app

ENTRYPOINT ["/usr/bin/ssserver", "-k12345678"]
