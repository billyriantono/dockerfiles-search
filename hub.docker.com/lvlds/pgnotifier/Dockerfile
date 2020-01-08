FROM golang:1.8.1-alpine

RUN apk update && apk upgrade && \
    apk add --no-cache git

RUN go get github.com/lib/pq
RUN go get github.com/streadway/amqp

ADD . /go/src/github.com/lvlds/pgnotifier/

WORKDIR /go/src/github.com/lvlds/pgnotifier/

ENV GOBIN /usr/bin
RUN go install main.go

CMD ["/usr/bin/main"]