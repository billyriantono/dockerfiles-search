FROM golang:1.6

RUN go get github.com/Krasnyanskiy/goaws

WORKDIR /go/src/github.com/Krasnyanskiy/goaws

RUN go build .

CMD ["goaws"]