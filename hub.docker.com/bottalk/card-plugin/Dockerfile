# Multi-stage build setup (https://docs.docker.com/develop/develop-images/multistage-build/)

# Stage 1 (to create a "build" image, ~850MB)
FROM golang:1.11 AS builder
RUN go version

COPY . /go/src/github.com/bottalk/bottalk-card-plugin
WORKDIR /go/src/github.com/bottalk/bottalk-card-plugin
RUN go get -v .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -o plugin .

# Stage 2 (to create a downsized "container executable", ~7MB)

FROM alpine:3.7
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/github.com/bottalk/bottalk-card-plugin/plugin .

EXPOSE 9081/tcp
ENTRYPOINT ["./plugin"]
