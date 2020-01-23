# Docker builder for Golang
FROM golang as builder
LABEL maintainer="Justin Barksdale"
WORKDIR ${GOPATH}/src/github.com/3pings/clWallEvents
COPY . .

RUN set -x && \
    go get -d -v . && \
    CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

# Get ca-certifcate
FROM alpine:latest as certs
RUN apk --update add ca-certificates

# Docker run Golang app
FROM scratch
LABEL maintainer="Justin Barksdale"
COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
WORKDIR /root/
COPY --from=builder /go/src/github.com/3pings/clWallEvents .
CMD ["./app"]