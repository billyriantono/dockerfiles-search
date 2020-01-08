FROM alpine:3.9

RUN set -ex; \
  \
  apk add --no-cache mono --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing ; \
  apk add --no-cache --virtual=.build-dependencies ca-certificates ; \
  cert-sync /etc/ssl/certs/ca-certificates.crt ; \
  apk del .build-dependencies
