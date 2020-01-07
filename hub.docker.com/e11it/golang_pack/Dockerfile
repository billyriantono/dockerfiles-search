FROM golang:1.11-alpine3.7

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
    
RUN    go get -u github.com/lib/pq \
    && go get -u github.com/roistat/go-clickhouse \
    && go get -u github.com/kshvakov/clickhouse
