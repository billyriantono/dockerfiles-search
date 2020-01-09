FROM alpine:edge
MAINTAINER Lars Nieuwenhuizen <l.nieuwenhuizen@developers.nl>

RUN apk update && \
    apk add yarn

RUN rm -rf /var/cache/apk/*

RUN mkdir -p /data

WORKDIR /data

ENTRYPOINT ["yarn"]