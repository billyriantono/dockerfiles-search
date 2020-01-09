FROM golang as builder
COPY . $GOPATH/src/gitlab.blockfin.us/hash/miner
WORKDIR $GOPATH/src/gitlab.blockfin.us/hash/miner
RUN go get -d -v && \
    CGO_ENABLED=0 go build -ldflags "-s -w" -o /go/bin/main
COPY configs/* /go/bin/

FROM scratch
COPY --from=builder /go/bin/* /go/bin/
WORKDIR /go/bin
ENTRYPOINT ["./main"]
CMD ["help"]
