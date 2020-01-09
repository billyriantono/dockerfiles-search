# syntax=docker/dockerfile:experimental

FROM golang:1-alpine AS builder
WORKDIR /usr/src/app

RUN apk add --update --no-cache \
  git ca-certificates tzdata curl \
  && rm -rf /var/cache/apk/*

COPY ./go.mod ./go.* ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 go build -o /go/bin/deploykit ./cmd/deploykit

FROM alpine:3.9

COPY --from=builder /usr/share/zoneinfo /usr/share/zoneinfo
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /go/bin/deploykit /bin/deploykit

ENV PORT=8080
EXPOSE $PORT
EXPOSE 6060

# The healthcheck is used by the routing mesh, during a rolling update, to
# understand when to avoid a container that isn't ready to receive traffic.
HEALTHCHECK --interval=5s --timeout=5s --start-period=2s --retries=5 \
    CMD curl -sS http://localhost:$PORT/health || exit 1

RUN addgroup -g 1000 -S deploykit && \
    adduser -u 1000 -S deploykit -G deploykit
USER deploykit

CMD ["deploykit"]
