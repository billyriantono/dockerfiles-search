FROM golang:latest as builder
WORKDIR /go/src/github.com/CommonSun/nsqd-discovery
COPY . .
RUN go get -u -v github.com/golang/dep/cmd/dep \
  && dep ensure -v \
  && CGO_ENABLED=0 go build -a --installsuffix cgo --ldflags="-s" -o nsqd-discovery

FROM centurylink/ca-certs
MAINTAINER Heymarket Team
WORKDIR /app
COPY --from=builder /go/src/github.com/CommonSun/nsqd-discovery/nsqd-discovery /app/nsqd-discovery
ENTRYPOINT ["./nsqd-discovery"]

