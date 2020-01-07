FROM golang:1.13.1-alpine3.10

RUN apk add --update git gcc libc-dev &&\
    go get gopkg.in/urfave/cli.v2 &&\
    go get github.com/oxequa/realize &&\
    go get -u github.com/rakyll/gotest &&\
    go get -u golang.org/x/tools/cmd/godoc &&\
    mkdir -p /tmp/example &&\
    ( cd /tmp/example; go mod init example; go get -u goa.design/goa/v3/cmd/goa ) &&\
    rm -rf /tmp/example &&\
    rm -rf /var/cache/apk/* &&\
    rm -rf /go/pkg/mod &&\
    echo

CMD godoc --http=0.0.0.0:8080
