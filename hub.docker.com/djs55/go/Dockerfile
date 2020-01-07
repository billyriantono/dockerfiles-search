FROM alpine:edge
RUN apk update && apk add alpine-sdk go git strace
ENV GOPATH=/go
WORKDIR /go
RUN go get -u github.com/golang/dep/cmd/dep
ENV PATH=$PATH:$GOPATH/bin
