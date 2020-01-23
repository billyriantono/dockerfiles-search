FROM golang:1.13 as builder

# Docker is copying directory contents so we need to copy them in same directories.
WORKDIR /go/src/github.com/stakater/ProxyInjector
COPY internal internal
COPY vendor vendor
COPY pkg pkg
COPY main.go main.go
# Other files can be copied into the WORKDIR.
COPY ["go*", "./"]

# Build the static application binary.
RUN GO111MODULE=on CGO_ENABLED=0 GOOS=linux go build -mod=vendor -a -installsuffix cgo --ldflags="-s" -o proxyinjector

# Create the final small image.
FROM alpine:3.9

RUN apk update && apk upgrade && \
    apk add --no-cache \
    ca-certificates \
    tzdata && \
    rm -rf /var/cache/apk/*

COPY --from=builder /go/src/github.com/stakater/ProxyInjector/proxyinjector /usr/bin/proxyinjector

CMD ["proxyinjector"]
