FROM alpine:3.8

RUN apk update && \
    apk add --no-cache ansible openssh && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*