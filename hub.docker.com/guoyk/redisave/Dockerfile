FROM golang:1.13 AS builder

ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.io
ENV CGO_ENABLED=0

WORKDIR /go/src/redisave

COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

FROM alpine:3.10

COPY --from=builder /go/bin/redisave /

CMD ["/redisave"]
