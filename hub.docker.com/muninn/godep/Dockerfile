FROM golang:alpine

RUN apk update && \
    apk add ca-certificates git

# install go dep
RUN go get -u github.com/golang/dep/cmd/dep
