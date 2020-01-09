FROM alpine:3.7

RUN apk add --no-cache ca-certificates && \
    apk add --no-cache curl

ENTRYPOINT ["/usr/bin/curl"]
