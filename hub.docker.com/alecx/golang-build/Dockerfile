FROM golang:1.12-alpine

ENV \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64 \
    GOMETALINTER=2.0.12 \
    GOLANGCI=1.16.0 

RUN \
    apk add --no-cache --update tzdata git bash curl && \
    cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
    rm -rf /var/cache/apk/*

RUN \
    go version && \
    go get -u -v github.com/alecthomas/gometalinter && \
    cd /go/src/github.com/alecthomas/gometalinter && \
    git checkout v${GOMETALINTER} && \
    go install github.com/alecthomas/gometalinter && \
    gometalinter --install && \
    go get -u -v github.com/GoASTScanner/gas && \
    go get -u -v github.com/golang/dep/cmd/dep && \
    go get -u -v github.com/kardianos/govendor && \
    go get -u -v github.com/jteeuwen/go-bindata/... && \
    go get -u -v github.com/stretchr/testify && \
    go get -u -v github.com/vektra/mockery/.../

RUN \
    go get -u -v github.com/golangci/golangci-lint/cmd/golangci-lint && \
    cd /go/src/github.com/golangci/golangci-lint && \
    git checkout v${GOLANGCI} && \
    cd /go/src/github.com/golangci/golangci-lint/cmd/golangci-lint && \
    go install -ldflags "-X 'main.version=$(git describe --tags)' -X 'main.commit=$(git rev-parse --short HEAD)' -X 'main.date=$(date)'" && \
    golangci-lint --version

ADD scripts/checkvendor.sh /script/checkvendor.sh
RUN chmod +x /script/checkvendor.sh
