FROM golang:1.13-alpine AS build

RUN apk add git

WORKDIR /go/src/github.com/joeds13/gmond_exporter
COPY . .

RUN go get -d -v ./...
RUN go build -v .

FROM alpine

COPY --from=build /go/src/github.com/joeds13/gmond_exporter/gmond_exporter /gmond_exporter

ENTRYPOINT ["/gmond_exporter"]
