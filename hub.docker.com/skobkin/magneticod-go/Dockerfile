FROM golang:1-alpine3.8 as builder

WORKDIR /go/src/github.com/boramalper/magnetico

ENV GOPATH=/go

RUN apk update && apk add \
    bash \
    gcc \
    git \
    libc-dev

RUN go get -u github.com/golang/dep/cmd/dep

RUN mkdir -p /go/src/github.com/boramalper/magnetico \
    && git clone -b go-rewrite --depth=1 https://github.com/boramalper/magnetico /go/src/github.com/boramalper/magnetico \
    && dep ensure \
    && echo 'func NewDecoder2(r interface {io.ByteScanner; io.Reader}) *Decoder {return &Decoder{r: r}}' \
    >> /go/src/github.com/boramalper/magnetico/vendor/github.com/anacrolix/torrent/bencode/api.go

RUN go install --tags fts5 "-ldflags=-s -w" ./cmd/magneticod

FROM alpine:3.8

WORKDIR /go/bin

RUN mkdir -p /data

COPY --from=builder /go/bin/magneticod .

ENTRYPOINT ["/go/bin/magneticod", "--trawler-ml-addr=0.0.0.0:64879", "--database=sqlite3:///data/database.sqlite3"]

EXPOSE 64879/udp
