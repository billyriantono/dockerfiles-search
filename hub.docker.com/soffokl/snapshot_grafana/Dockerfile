FROM golang:1.13-alpine AS builder

# Install application
WORKDIR /go/src/github.com/soffokl/snapshot_grafana
ADD . .

# Build application
RUN go build -o snapshot_grafana main.go

FROM alpine:latest

COPY --from=builder /go/src/github.com/soffokl/snapshot_grafana/snapshot_grafana /snapshot_grafana
ENTRYPOINT ["/snapshot_grafana"]
