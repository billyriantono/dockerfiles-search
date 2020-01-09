FROM golang:1-alpine

RUN apk update && \
    apk add curl git

RUN curl https://glide.sh/get | sh
RUN go get -u github.com/jstemmer/go-junit-report
