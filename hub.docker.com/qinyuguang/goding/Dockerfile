FROM golang:1.13-alpine

WORKDIR /go/src

ADD . .

RUN go build -o main .

CMD ["./main -e online"]
