FROM golang:1.10-alpine

RUN apk -v --update add \
        git \
        gcc \
        libc-dev \
        && \
    rm /var/cache/apk/*


RUN go get -u github.com/pressly/goose/cmd/goose && \
    wget -O /usr/local/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 && \
    chmod +x /usr/local/bin/jq

ENTRYPOINT []