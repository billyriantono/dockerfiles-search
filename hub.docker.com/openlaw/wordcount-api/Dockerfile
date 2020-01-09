FROM golang:1.10 AS builder
RUN mkdir -p /go/src/github.com/openlawteam/wordcount-api-go
WORKDIR /go/src/github.com/openlawteam/wordcount-api-go
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
	go build -ldflags "-s -w" -a -installsuffix cgo -o wordcount-api

FROM alpine:latest
RUN apk --no-cache add ca-certificates curl
WORKDIR /root/
COPY --from=0 /go/src/github.com/openlawteam/wordcount-api-go/wordcount-api .
ENV PORT=8001
HEALTHCHECK --interval=1m --timeout=3s \
  CMD curl -f http://localhost:${PORT}/health-check || exit 1
CMD ["./wordcount-api"]
