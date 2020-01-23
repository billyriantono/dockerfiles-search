FROM golang:latest

MAINTAINER hexiaopi "Hexiaopi0619@163.com"

WORKDIR $GOPATH/src/github.com/Hexiaopi/go-patterns-example

ADD . $GOPATH/src/github.com/Hexiaopi/go-patterns-example

RUN ls

CMD go build ./strategy/main.go

ENTRYPOINT [".main"]