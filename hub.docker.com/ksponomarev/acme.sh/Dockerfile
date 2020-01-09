FROM alpine:latest

RUN set -ex; \
    apk add --no-cache openssl curl; \
    curl https://get.acme.sh | sh

WORKDIR /root/.acme.sh