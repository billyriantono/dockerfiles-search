FROM alpine:3.7
MAINTAINER Guillermo Rodríguez Cano <gurc@kth.se>

ENV PACKAGES="bash \
              curl"

RUN apk add --no-cache --update \
        ${PACKAGES} \
    && rm -rf /var/cache/apk/*
