FROM golang

RUN go get -v \
    github.com/docker/docker/api/types \
    github.com/docker/docker/client \
    golang.org/x/net/context \
    github.com/gorilla/websocket \
    github.com/gomodule/redigo/redis \
    github.com/kballard/go-shellquote

WORKDIR /go/src/app
COPY ./src .

RUN go get -d -v ./...
RUN go install -v ./...

EXPOSE 80
CMD ["app"]