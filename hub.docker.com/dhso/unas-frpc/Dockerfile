FROM alpine:3.8
MAINTAINER dhso <dhso@163.com>

RUN mkdir -p /app

WORKDIR /app

COPY frpc frpc
COPY frpc.ini frpc.ini
RUN chmod +x frpc

ENTRYPOINT ./frpc -c frpc.ini