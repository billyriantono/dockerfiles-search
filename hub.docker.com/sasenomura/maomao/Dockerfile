FROM golang:1.13-alpine as build

COPY ./ /go/src/github.com/MaoMao
WORKDIR /go/src/github.com/MaoMao

RUN GOOS=linux GOARCH=amd64 go build app/main.go

FROM alpine:3.8
COPY --from=build /go/src/github.com/MaoMao/main /bin/provider

# provider