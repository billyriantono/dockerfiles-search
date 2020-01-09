FROM golang:1.8

LABEL maintainer "d.chupin@movavi.com"

ADD . /go/src/github.com/chupindo/webhooks

RUN go get github.com/gorilla/mux
RUN go install github.com/chupindo/webhooks

ENTRYPOINT ["/go/bin/webhooks"]

EXPOSE 8080