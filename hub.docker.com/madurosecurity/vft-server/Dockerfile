FROM golang:1.11-alpine as builder
WORKDIR /go/src/github.com/madurosecurity/vft-server
COPY . .
RUN apk --no-cache add build-base

# Build and pack server
RUN go build -ldflags="-s -w" -o /go/bin/vft-server .

# Install binaries
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/bin/vft-server /go/bin/vft-server
ENTRYPOINT ["/go/bin/vft-server"]
