#############################
## STEP 1 build executable binary
#############################
FROM golang:alpine AS builder
ENV CGO_ENABLED 0
ENV GOOS linux
ENV GOARCH amd64

# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git
COPY . $GOPATH/src/github.com/pjvds/streamsdb
WORKDIR $GOPATH/src/github.com/pjvds/streamsdb
# Fetch dependencies.

# Build the binary.
RUN cd cli && go build -a -installsuffix cgo -ldflags="-w -s" -o /go/bin/sdbcli
ENTRYPOINT ["/go/bin/sdbcli"]

