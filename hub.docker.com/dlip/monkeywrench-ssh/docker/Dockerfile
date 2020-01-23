FROM golang:alpine as builder

RUN apk add --no-cache git \
    && go get -u github.com/rakyll/hey

FROM alpine:3.7

COPY --from=builder /go/bin/hey /app/hey

ENTRYPOINT ["/app/hey"]
