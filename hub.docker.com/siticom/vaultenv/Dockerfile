FROM golang:1.13-alpine AS builder

ADD . /go/src/github.com/siticom/vaultenv

WORKDIR  /go/src/github.com/siticom/vaultenv

RUN CGO_ENABLED=0 go build -o /go/bin/vaultenv main.go

FROM alpine

RUN apk add --update --no-cache ca-certificates

COPY --from=builder /go/bin/vaultenv /vaultenv

ENTRYPOINT ["/vaultenv"]
