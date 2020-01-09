FROM golang:1.13-alpine AS builder
ENV GO111MODULE=on
# 替换原始apk地址
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
# 安装必备软件
RUN apk add upx make git
# 设置工作目录
WORKDIR /go/src/github.com/kaisawind/broker.websocket
# 设置GO代理
RUN go env -w GOPROXY=https://goproxy.io
COPY . .
RUN make
RUN cp ./bin/websocket ./bin/main
RUN upx ./bin/main

FROM alpine

LABEL MAINTAINER="kaisawind <wind.kaisa@gmail.com>"

COPY --from=builder /go/src/github.com/kaisawind/broker.websocket/bin/main / 
COPY --from=builder /go/src/github.com/kaisawind/broker.websocket/scripts/config-prod.yaml /broker/

USER 6342627

# GRPC
EXPOSE 9090
# HTTP
EXPOSE 8080

CMD ["/main","--host=0.0.0.0","--port=8080"]
