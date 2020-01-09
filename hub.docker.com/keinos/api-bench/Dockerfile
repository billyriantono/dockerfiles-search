FROM golang:alpine AS build

RUN apk add --no-cache \
      git gcc g++ && \
    git clone https://github.com/rakyll/hey.git hey && \
    cd hey && \
    go build \
      -a \
      --ldflags '-extldflags "-static"' \
      -o /go/bin/hey \
      hey.go && \
    go test

FROM keinos/alpine:latest
COPY --from=build /go/bin/hey /usr/local/bin/hey

ENTRYPOINT ["/usr/local/bin/hey"]
