FROM golang:1.9 AS builder

#RUN apk update && apk add ca-certificates
RUN curl -fsSL -o /usr/local/bin/dep https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64 && chmod +x /usr/local/bin/dep
RUN mkdir -p /go/src/github.com/***

COPY . $GOPATH/src/github.com/wowgroup/go-sla/
WORKDIR $GOPATH/src/github.com/wowgroup/go-sla

RUN dep ensure 
#-vendor-only
RUN make build-linux

FROM busybox:latest
COPY --from=builder /go/bin/sla /go/bin/sla_unix
COPY --from=builder /etc/ssl/certs /etc/ssl/certs
ADD https://gist.githubusercontent.com/Inquizarus/be8d3a133e52c2a966256a11c33c7565/raw/74e5355c017fcac59b6dd773462fb381754ddc06/sla.json /go/bin

WORKDIR /go/bin
ENTRYPOINT ["./sla"]
