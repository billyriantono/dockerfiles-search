FROM alpine:3.2

RUN apk update && \
    apk upgrade && \
    apk add bash && \
    apk add nano && \
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

ENTRYPOINT bash
