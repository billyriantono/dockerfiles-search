FROM alpine:edge

LABEL maintainer="S-Kazuki<contact@revoneo.com>"

RUN apk update \
  && apk add tzdata \
  && TZ=${TZ:-Asia/Tokyo} \
  && cp /usr/share/zoneinfo/$TZ /etc/localtime \
  && echo $TZ> /etc/timezone \
  && apk del tzdata \
  && rm -rf /var/cache/apk/*
