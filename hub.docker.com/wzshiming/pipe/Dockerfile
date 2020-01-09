FROM golang:1.10-alpine3.7 AS builder
ENV GOPATH=/tmp/gopath/
ENV GOBIN=$GOPATH/bin/
RUN apk add -U git
RUN go get -u -v github.com/wzshiming/pipe/cmd/pipe

FROM alpine:3.7
COPY --from=builder /tmp/gopath/bin/pipe /usr/local/bin/

ENTRYPOINT [ "pipe" ]