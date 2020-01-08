FROM golang:1.13-alpine AS build
RUN apk add --no-cache git
RUN go get github.com/google/safebrowsing/cmd/sbserver

FROM alpine:3.10
RUN apk add --no-cache ca-certificates
COPY --from=build /go/bin/sbserver /usr/bin/
CMD /usr/bin/sbserver -srvaddr 0.0.0.0:8080 -apikey $APIKEY
