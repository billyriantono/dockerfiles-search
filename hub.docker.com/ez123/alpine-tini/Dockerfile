FROM alpine:3.6

RUN apk add --no-cache tini bash

ENTRYPOINT ["/sbin/tini", "--"]
