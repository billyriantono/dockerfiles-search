ARG BASE_IMAGE_BUILDER=golang
ARG ALPINE_VERSION=3.10
ARG GO_VERSION=1.13

FROM ${BASE_IMAGE_BUILDER}:${GO_VERSION}-alpine${ALPINE_VERSION} AS builder
ARG GOARCH=amd64
ARG GOARM
RUN apk --update add git build-base
WORKDIR /tmp/gobuild
COPY go.mod go.sum ./
RUN go mod download 2>&1
COPY main.go .
RUN go test -v ./...
RUN CGO_ENABLED=0 GOOS=linux GOARCH=${GOARCH} GOARM=${GOARM} go build -ldflags="-s -w" -o app

FROM scratch
ARG BUILD_DATE
ARG VCS_REF
LABEL \
    org.opencontainers.image.authors="quentin.mcgaw@gmail.com" \
    org.opencontainers.image.created=$BUILD_DATE \
    org.opencontainers.image.version="" \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.url="https://github.com/qdm12/qr" \
    org.opencontainers.image.documentation="https://github.com/qdm12/qr/blob/master/README.md" \
    org.opencontainers.image.source="https://github.com/qdm12/qr" \
    org.opencontainers.image.title="qr" \
    org.opencontainers.image.description="Generates QR code in your terminal" \
    image-size="1.56MB"
ENTRYPOINT ["/qr"]
USER 1000
COPY --from=builder --chown=1000 /tmp/gobuild/app /qr
CMD ["--help"]