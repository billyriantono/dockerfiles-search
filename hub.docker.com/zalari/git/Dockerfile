FROM alpine

LABEL maintainer Christian Ulbrich <christian.ulbrich@zalari.de>

RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*
