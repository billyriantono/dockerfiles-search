FROM golang:alpine as builder

RUN \
  apk add --update --no-cache git ca-certificates && update-ca-certificates && \
  go get -d github.com/mayflower/unifi_exporter/cmd/unifi_exporter && \
  cd $GOPATH/src/github.com/mayflower/unifi_exporter/cmd/unifi_exporter && \
  CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/unifi_exporter

FROM scratch

COPY --from=builder /go/bin/unifi_exporter /go/bin/unifi_exporter
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

EXPOSE 9130

VOLUME /config
ENTRYPOINT ["/go/bin/unifi_exporter","-config.file","/config/config.yaml"]
