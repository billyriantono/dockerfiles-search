FROM alpine:latest

RUN apk add --upgrade \
    makepasswd && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["makepasswd"]
