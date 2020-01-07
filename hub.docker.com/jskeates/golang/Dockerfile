FROM golang:1.9.2-alpine

RUN apk add --no-cache git make protobuf bash curl ca-certificates \
 && curl -L -s https://github.com/golang/dep/releases/download/v0.3.2/dep-linux-amd64 -o $GOPATH/bin/dep \
 && chmod +x $GOPATH/bin/dep \
 && go get github.com/codegangsta/gin

ENTRYPOINT ["/bin/bash"]
