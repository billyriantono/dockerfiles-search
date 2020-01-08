FROM golang:alpine AS builder

# Install git.
# Git is required for fetching the dependencies.
RUN apk update && apk add --no-cache git
WORKDIR $GOPATH/src/heketi-ui

COPY . .
# Build the binary.
RUN go build -o /go/bin/server cmd/heketi-ui/server.go 

FROM gluster/glusterfs-client:latest

COPY --from=builder /go/bin/server /go/bin/server

# Command to run a container with the capabilities to mount glusterfs volumes
#  docker run -ti --rm --cap-add SYS_ADMIN --device /dev/fuse gluster/glusterfs-client bash