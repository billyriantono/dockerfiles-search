FROM golang:1.10-alpine
WORKDIR /usr/golang
RUN apk --no-cache add git gcc libc-dev && go get github.com/constabulary/gb/... && go get -u github.com/pressly/goose/cmd/goose
