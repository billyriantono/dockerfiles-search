FROM golang:1.13-alpine AS builder

RUN apk add --update --no-cache ca-certificates

ADD . /go/src/github.com/siticom/vaultenv

WORKDIR  /go/src/github.com/siticom/vaultenv/webhook

RUN CGO_ENABLED=0 go build -o /go/bin/vault-webhook main.go

FROM scratch

COPY --from=builder /go/bin/vault-webhook /vault-webhook
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

ENV DEBUG false
ENV VAULT_ADDR "vault.example.com"
ENV VAULT_CA_SECRET "vault-ca"
ENV VAULTENV_IMAGE "siticom/vaultenv"

ENTRYPOINT ["/vault-webhook"]
