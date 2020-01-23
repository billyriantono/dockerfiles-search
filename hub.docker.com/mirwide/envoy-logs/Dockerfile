FROM golang:alpine AS builder

# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git

WORKDIR /app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

# Build the binary.
RUN CGO_ENABLED=0 GOOS=linux go build -o envoy-logs

FROM ubuntu:18.04

# Copy our static executable.
COPY --from=builder /app/envoy-logs /app/envoy-logs
COPY resource  /resource

# Run the binary.
ENTRYPOINT ["/app/envoy-logs"]
