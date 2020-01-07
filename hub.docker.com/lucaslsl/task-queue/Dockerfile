FROM golang:1.7.4-alpine

COPY vendor /go/src/

COPY . /go/src/github.com/lucaslsl/task-queue

WORKDIR /go/src/github.com/lucaslsl/task-queue 

RUN go build -o main . 

CMD ["/go/src/github.com/lucaslsl/task-queue/main"]