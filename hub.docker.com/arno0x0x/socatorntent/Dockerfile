FROM alpine:3.3

RUN apk update && apk upgrade && \
    apk add --no-cache \
    ca-certificates \
    bash \
    git \
    openssh \
    curl \
    rsync && \
    rm -rf /var/cache/apk/*
