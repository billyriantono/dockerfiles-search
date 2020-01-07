FROM golang:1.8.3-alpine

WORKDIR /go/src/github.com/tebeka/go2xunit
COPY . /go/src/github.com/tebeka/go2xunit

RUN go install -v -ldflags="-s -w"
RUN go test -c -ldflags="-s -w"

ENTRYPOINT ["/go/bin/go2xunit"]
