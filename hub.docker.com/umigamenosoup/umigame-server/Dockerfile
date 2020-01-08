FROM golang:1.12.1-alpine3.9

RUN apk update && \
    apk add --no-cache git && \
    apk add --no-cache make

COPY ./server /go/src/github.com/umigamenosoup/umigame-server/server
ENV GO111MODULE=on

WORKDIR /go/src/github.com/umigamenosoup/umigame-server/server

RUN go get github.com/pilu/fresh

CMD ["make", "run"]

