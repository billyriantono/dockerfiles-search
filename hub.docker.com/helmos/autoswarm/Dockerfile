FROM golang:alpine as builder
RUN apk add git upx
RUN  go get -u github.com/grandcat/zeroconf \
&&   go get -u github.com/docker/docker/api/types/swarm \
&&   go get -u github.com/docker/docker/client \
&&   go get -u github.com/hashicorp/go-sockaddr
COPY autoswarm.go ./autoswarm.go
RUN CGO_ENABLED=0 GOOS=linux go build -o autoswarm.amd64 -a -ldflags '-s -w -extldflags "-static"' autoswarm.go \
&&   upx -9 autoswarm.amd64
  
FROM busybox
COPY --from=builder /go/autoswarm.amd64 /autoswarm
ENTRYPOINT ["/autoswarm"]
