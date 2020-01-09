FROM wizjin/gobuild:latest as builder

RUN echo build shadowsocks \
  && CGO_ENABLED=0 go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server \
  && CGO_ENABLED=0 go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local

FROM alpine:latest

MAINTAINER WizJin <wizjin@users.noreply.github.com>

COPY --from=builder /go/bin/shadowsocks-server /
COPY --from=builder /go/bin/shadowsocks-local /
