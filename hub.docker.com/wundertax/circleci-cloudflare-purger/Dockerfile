FROM golang:1.7.3 as builder
WORKDIR /go/src/github.com/wundertax/circleci-cloudflare-purger/
RUN go get -d -v github.com/cloudflare/cloudflare-go
COPY main.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o purger .

FROM alpine:latest  

RUN apk --no-cache add ca-certificates

LABEL maintainer "Wundertax Tech <devops@wundertax.de>" \
      org.label-schema.name = "circleci-cloudflare-purger" \
      org.label-schema.description = "Cloudflare purger, to be used with CircleCI." \
      org.label-schema.vendor = "Wundertax GmbH" \
      com.circleci.preserve-entrypoint=true

WORKDIR /

COPY --from=builder /go/src/github.com/wundertax/circleci-cloudflare-purger/purger /usr/bin/purger

ENTRYPOINT purger
