FROM golang:1.12-stretch as builder

ENV GO111MODULE on
WORKDIR /go/src/homekit-spotify

COPY Makefile .
COPY go.mod .
COPY go.sum .
RUN go mod download

COPY . .
RUN make build

FROM alpine as release

RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
    ca-certificates \
    && update-ca-certificates 2>/dev/null || true

COPY --from=builder /go/src/homekit-spotify/build/homekit-spotify /homekit-spotify

ADD config.json.template /config.json

ENTRYPOINT ["/homekit-spotify"]