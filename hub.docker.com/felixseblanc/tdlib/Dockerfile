FROM felixseblanc/tdlib:latest

ENV GO111MODULE on
ENV GO_TDLIB_VERSION 0.1.0

RUN go get github.com/zelenin/go-tdlib@v${GO_TDLIB_VERSION}

WORKDIR $GOPATH