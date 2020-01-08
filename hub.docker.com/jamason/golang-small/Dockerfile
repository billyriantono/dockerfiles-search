FROM golang:1.9
RUN mkdir -p /go/src
WORKDIR /go/src
COPY count.go .
RUN go build -ldflags "-linkmode external -extldflags -static" -a count.go
FROM scratch
COPY --from=0 /go/src/count count
CMD ["/count"]
