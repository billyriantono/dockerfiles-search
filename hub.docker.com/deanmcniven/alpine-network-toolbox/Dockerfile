FROM alpine:latest
MAINTAINER deanmcniven@users.noreply.github.com

ENV TZ="Australia/Sydney"

RUN apk update && \
    apk add bind-tools busybox-extras tcpdump tzdata && \
    rm -rf /var/cache/apk/*

CMD /bin/sh
