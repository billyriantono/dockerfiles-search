FROM golang:1.9-alpine

ENV USER app

COPY ca.crt.pem /etc/tls/ca.crt.pem

RUN addgroup -S $USER && adduser -Sg $USER $USER && \
    mkdir -p bin pkg src && \
    chown -R $USER:$USER . && \
    apk add --update curl && \
    rm -rf /var/cache/apk/*

RUN chown app:app /etc/tls/ca.crt.pem

USER $USER
