ARG GO_VERSION=1.12

FROM golang:${GO_VERSION}-alpine AS builder

RUN apk add --update --no-cache git

RUN mkdir -p /build
WORKDIR /build

COPY go.* ./
RUN go mod download

COPY . .
RUN go build


FROM alpine:3.9

COPY --from=builder /build/helm-push-filter /

CMD ["/helm-push-filter"]
