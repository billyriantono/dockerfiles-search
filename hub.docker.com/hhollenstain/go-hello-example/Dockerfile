FROM golang:1.8.0-alpine

ENV SRC_DIR=/go/src/github.com/hhollenstain/go-hello-example
COPY ./ $SRC_DIR
WORKDIR $SRC_DIR
RUN go build -o main .
CMD ["/go/src/github.com/hhollenstain/go-hello-example/main"]
