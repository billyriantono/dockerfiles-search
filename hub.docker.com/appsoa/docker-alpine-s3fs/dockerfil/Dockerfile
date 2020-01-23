FROM golang:1.13 as builder
WORKDIR /go/src
COPY . .
RUN CGO_ENABLED=0 go build -v -ldflags="-s -w -X github.com/coredns/coredns/coremain.GitCommit=$(shell git describe --dirty --always)" -o coredns

FROM debian:stable-slim as certs

RUN apt-get update && apt-get -uy upgrade
RUN apt-get -y install ca-certificates && update-ca-certificates

FROM scratch

COPY --from=certs /etc/ssl/certs /etc/ssl/certs
COPY --from=builder /go/src/coredns /coredns

EXPOSE 53 53/udp
ENTRYPOINT ["/coredns"]
