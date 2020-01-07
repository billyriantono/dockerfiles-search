FROM golang

COPY . /go/src/github.com/nkumar15/golang-chat

RUN go get github.com/gorilla/websocket

RUN go install github.com/nkumar15/golang-chat/chat

WORKDIR /go/src/github.com/nkumar15/golang-chat/chat

ENTRYPOINT /go/bin/chat

EXPOSE 8080
