FROM golang:1.9.4-alpine3.7 as builder
WORKDIR /go/src/auth-proxy
ADD . .

RUN \
  apk update &&\
  apk add git &&\
  go get -d 

RUN go build .

FROM alpine

COPY --from=builder /go/src/auth-proxy/auth-proxy /auth-proxy

RUN \
set -ex \
   && apk add --no-cache ca-certificates

CMD ["/auth-proxy"]