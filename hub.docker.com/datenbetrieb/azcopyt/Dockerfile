FROM golang:1.13-alpine as builder

ENV GOPATH="/go" \
    CGO_ENABLED="0"

ADD . /go/src/github.com/datamachines/podlike
WORKDIR /go/src/github.com/datamachines/podlike

RUN apk update && \
    apk add git dep && \
    dep ensure && \
    go install -v ./...

# Pivot to smaller image without build tools.
FROM alpine:latest

ARG VERSION="dev"
ARG BUILD_ARCH="unknown"
ARG GIT_COMMIT="unknown"
ARG BUILD_TIMESTAMP="unknown"

ENV VERSION="$VERSION" \
    BUILD_ARCH="$BUILD_ARCH" \
    GIT_COMMIT="$GIT_COMMIT" \
    BUILD_TIMESTAMP="$BUILD_TIMESTAMP"

LABEL maintainer="Chris Monson <chrismonson@datamachines.io>" \
      com.github.datamachines.podlike.version="$VERSION" \
      com.github.datamachines.podlike.commit="$GIT_COMMIT"

RUN apk --no-cache add ca-certificates openssl curl bash

COPY --from=builder /go/bin/* /usr/local/bin/

# TODO: should this reference hc above?
HEALTHCHECK --interval=2s --timeout=3s --retries=5 CMD [ "podlike", "healthcheck" ]

ENTRYPOINT ["podlike"]
