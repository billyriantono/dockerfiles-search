FROM golang:1.10-alpine

# install dependencies
RUN apk --update upgrade && \
    apk add sqlite wget unzip make git coreutils gcc libc-dev && \
    rm -rf /var/cache/apk/*
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
RUN go get -u -v github.com/golang/dep/cmd/dep
RUN go get -u -v github.com/mailru/easyjson/...
