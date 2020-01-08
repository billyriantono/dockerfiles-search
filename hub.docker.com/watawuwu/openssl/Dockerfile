FROM alpine:3.7

RUN apk add --update openssl ca-certificates bash curl

ENV \
  SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt \
  SSL_CERT_DIR=/etc/ssl/certs

