FROM golang:alpine as builder
EXPOSE 80 443 5223

RUN mkdir -p /go/src/github.com/mmatczuk/go-http-tunnel
ADD . /go/src/github.com/mmatczuk/go-http-tunnel
RUN go install github.com/mmatczuk/go-http-tunnel/cmd/...

ENTRYPOINT ["/go/bin/tunneld"]
