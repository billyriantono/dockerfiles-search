FROM golang:1.12-rc-alpine3.9 as builder
RUN set -eux; \
    apk add --no-cache git; \
    go get -u github.com/sethvargo/go-password/password
WORKDIR /go/src/app
COPY passgen.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -o passgen .

FROM alpine:3.9
COPY --from=builder /go/src/app/passgen /app/
ENTRYPOINT ["/app/passgen"]
