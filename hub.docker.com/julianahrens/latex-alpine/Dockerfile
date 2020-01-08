FROM alpine:3.10.3

RUN apk update && \
    apk add --no-cache biber && \
    apk add --no-cache texlive-full && \
    rm -rf /var/cache/apk/*
