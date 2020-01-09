FROM golang:1.11

RUN git clone https://github.com/pingcap/tidb-tools.git src/github.com/pingcap/tidb-tools

RUN go get github.com/pingcap/tidb/types

COPY Makefile /go/src/github.com/pingcap/tidb-tools

WORKDIR /go/src/github.com/pingcap/tidb-tools

RUN go clean -modcache

RUN make

