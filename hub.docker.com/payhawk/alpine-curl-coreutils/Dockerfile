FROM alpine:3.10

RUN apk add --no-cache curl

RUN apk add --update coreutils && rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/bin/curl"]