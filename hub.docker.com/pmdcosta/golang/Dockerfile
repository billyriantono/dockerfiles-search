FROM golang:1.11-alpine

# Install git
RUN apk add --no-cache git

# Download and install dep
ADD https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64 /usr/bin/dep
RUN chmod +x /usr/bin/dep
