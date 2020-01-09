# stage 1 - build process
#
FROM golang:1.10.3-alpine as builder

ARG SRC_PATH=/go/src/bitbucket.org/game-labs/data-storage
WORKDIR $SRC_PATH

RUN apk add --no-cache git dep make

COPY Gopkg.toml Gopkg.lock Makefile ./
RUN dep ensure -vendor-only

COPY ./pkg ./pkg
RUN CGO_ENABLED=0 go build -a -v -o /tmp/storage pkg/cmd/storage/*.go

# stage 2 - build docker image
#
FROM alpine:3.8

WORKDIR /app
COPY --from=builder /tmp/storage .

CMD ["/app/storage"]
