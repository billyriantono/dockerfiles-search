FROM golang:1.13-alpine AS go-builder

# Replicate the APK repository override.
# If it is no longer necessary to avoid the CDN mirros we should consider dropping this as it is brittle.
RUN sed -e 's/dl-cdn[.]alpinelinux.org/mirrors.aliyun.com/g' -i~ /etc/apk/repositories
# Install our build time packages.
RUN apk add --no-cache build-base git openssh-client upx
# go proxy
RUN go env -w GOPROXY=https://goproxy.io

WORKDIR $GOPATH/src/github.com/kaisawind/template.go

COPY go.mod .
RUN go mod download

COPY . .

RUN make build
RUN upx bin/apiserver
RUN upx bin/monitor
RUN chmod 755 scripts/docker-entrypoint.sh

FROM alpine:3.8

LABEL MAINTAINER="kaisawind <wind.kaisa@gmail.com>"

COPY --from=go-builder /go/src/github.com/kaisawind/template.go/bin/ /template/
COPY --from=go-builder /go/src/github.com/kaisawind/template.go/scripts/certs/ /template/certs/
COPY --from=go-builder /go/src/github.com/kaisawind/template.go/scripts/config-prod.yaml /template/config-prod.yaml
COPY --from=go-builder /go/src/github.com/kaisawind/template.go/scripts/docker-entrypoint.sh /entrypoint.sh

EXPOSE 8080

ENTRYPOINT ["/entrypoint.sh"]