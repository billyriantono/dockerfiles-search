FROM alpine:latest

RUN apk add --no-cache openssl bash

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

