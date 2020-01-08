FROM golang:latest as builder
WORKDIR /dler-server-src
COPY . /dler-server-src
RUN go mod download && \
    GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -ldflags '-w -s' -o /dler-server

FROM alpine:latest
COPY --from=builder /dler-server /
ENTRYPOINT ["/dler-server"]
