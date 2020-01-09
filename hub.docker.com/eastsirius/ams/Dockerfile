FROM golang:1.12.5-alpine3.9 as builder-go
COPY . /go/src/ams
WORKDIR /go/src/ams
RUN set -ex && go build .

FROM alpine:3.9
COPY --from=builder-go /go/src/ams/ams /usr/local/bin/ams
WORKDIR /var/ams
CMD ams
