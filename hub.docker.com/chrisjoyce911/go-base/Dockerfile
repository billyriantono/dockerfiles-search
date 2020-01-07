FROM golang:1.13 AS build

ENV GO111MODULE=on
ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64
ENV RICHGO_FORCE_COLOR 1
ENV RICHGO_LOCAL 1
WORKDIR /workspace

# Packages with fixed versions
RUN go get github.com/kyoh86/richgo@v0.3.3
RUN go get github.com/golangci/golangci-lint/cmd/golangci-lint@v1.19.1

# Go tools/dependencies
# ARG GOPROXY=direct
ADD go.mod go.mod
ADD go.sum go.sum
RUN go mod download

