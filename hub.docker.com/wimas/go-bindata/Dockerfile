FROM amd64/golang:1.13.4

RUN go get -u github.com/jteeuwen/go-bindata/ && \
    go get -u github.com/jteeuwen/go-bindata/go-bindata && \
    go install github.com/jteeuwen/go-bindata/go-bindata

CMD ["go-bindata", "--help"]
