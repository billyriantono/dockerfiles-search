FROM golang:1.12-alpine
MAINTAINER sangx2

RUN apk add gcc g++ git

WORKDIR /go/src/github.com/sangx2/exim/

COPY . .
RUN go get -d -v ./...;go install -v ./...
RUN go build -o exim.ex ./cmd/main.go

CMD ./exim.ex
